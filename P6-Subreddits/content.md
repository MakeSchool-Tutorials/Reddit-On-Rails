# Creating Subreddits

## Teacher Steps

Make sure that students have merged their user model into the development branch, that both pairs have run migrations. They should be able to create a user object and delete a user object.

## Making sure everyone is on the same page.

This is the point where if you wanted to split off your work you should be able to have one partner work on authentication and the other working on subreddits!

Make sure that all your environments are setup to be the same and everyone has the same migrations. We'll create a new feature branch for this section called 'subreddits'.

## Creating the model

We can use our scaffolding to generate our subreddits too. But let's review what's necessary for a subreddit? What fields does a sub reddit know and what relationships does it have to other objects?

The primary thing we care about is that each subreddit has a name and is created by a certain user. So our model needs at least two fields. It also has posts but let's worry about that another time. We're going to add that later with a later migration.

Instead of specifying string or int we can use scaffold generate to make it a reference.

```
	rails generate scaffold Subreddit name:string creator:references
```

You can see now that we have our model automatically generate the field, but it adds an index on it so that we can ensure that we mantain the relationship. You can now see that we can create subreddits and visit other pages.

## Adding Validation

We're going to need validate a few things for our subreddits though before we continue on. We should review about Rails Validations here on this page: [http://guides.rubyonrails.org/active_record_validations.html](Validations)

We're going to add uniqueness constraint to our subreddit name to ensure that people don't create multiple subreddits with the same name.

We're also going to ensure that every subreddit has a maximum_length of 21 characters, only consists of letters, numbers, and whitespace.


## Slugs

You'll notice on reddit that the URL for a sub reddit is something like https://www.reddit.com/r/funny, where the name of the subreddit is in the URL. The concept of having urls that route to the names of an object in your database is a concept called 'slugs'. Slugs are useful because they're more memorable urls. I'll remember reddit.com/r/funny but it's harder to remember reddit.com/r/551851 which is how default routing works in Rails.

But we don't want to use the name field in our subredit model, people might create names of subreddits that don't work in URLS, any subreddit with a space won't work! So we need to create our own slug field properly.

1. Adding the slug

Let's create a new field in our subredit model called slugs. It should be a string with all the same validations as our names, but we're going to be more restrictive. Don't allow the slug to have any whitespace characters since those are not legal in a URL.

2. Create a method that creates the slug in our model.

We're going to need a method that translates the name into a slug. So let's create a method that strips all the whitespace form the name so that you can create a slug. Create this method in the model.

But we also don't want the user to have to type in a slug, we just want the slug to be automatically there when we create or modify a subreddit. Thankfully ActiveRecord provides a nice tool for this called [http://api.rubyonrails.org/classes/ActiveRecord/Callbacks.html](ActiveRecord callbacks).

We're going to add our own after save callback to ensure that we translate the name into the slug column properly. To make sure the changes propagate to our database. We need to call self.update_attributes() which will update database columns without calling further callbacks. If we just modified the column and save we would get into an infinite loop!

3. Set up your own route

So let's create our own slugs. The first step that we'll do is create our route in the routes.rb. If you look over what we have now we'll see that it's mostly resources. We'll be adding our own matcher. You can read more about routing [http://guides.rubyonrails.org/routing.html](here).

But for now let's add a route that matches r/subreddit_name and send that to controller method in our subreddits controller show.

3. Find the subreddit in your show controller

We should be able to find the subreddit based on the name from the routing parameter. Use our model method finders to find the subreddit by the name. Everything should display as before but how should work when you visit localhost:3000/r/subreddit_name

4. Improving performance

One of the downsides of slugs is that we have to make sure that it's performance. When you visit /subreddit/1 it's pretty fast to look up the subreddit in our database because we are looking it up by the primary key. But now we're looking for our subreddits by the name and thus we need to be a string comparison against all the other names in order to find it. The database right now is small so it's not a big performance impact but we'll see about adding an **index**.

If you don't know about indexes already, they are a database concept in which we ask the database to keep a separate data structure that allows us to search a field quickly. The cost of maintaining the index is whenever you create, delete or modify an entry there will be some additional cost because of each index.

So the next cost will be adding our index to the table. We're going to add an index to our slug column. Let's create a new migration and use the add_index command.

If you try to run the migration though, you might run into an issue. Indexes can't be added to a column when it has empty columns. This is a good time to learn about backfilling a column. We'll run into this situation many times in production code, sometimes we want to add something new but provide some kind of default code that populates something.

So let's modify our migration file and include some code that goes through all the subreddit objects and generates their slug based on their name. Then we can add our index appropriately. Because of our after save callback we won't have to worry future models, just our existing ones.