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

We're going to need validate a few things for our subreddits though before we continue on. We should learn about Rails Validations here on this page: http://guides.rubyonrails.org/active_record_validations.html

We're going to add uniqueness constraint to our subreddit name to ensure that people don't create multiple subreddits with the same name. 

We're also going to ensure that every subreddit has a maximum_lenght of 21 characters, only consists of letters, numbers, and underscores. You'll notice on reddit that the URL for a sub reddit is something like https://www.reddit.com/r/funny, where the name of the subredit is in the URL. These validations allow us to simplify our logic for creating that since many other characters outside of underscores, letters and numbers have to be escaped in URLs. Anytime you're using creating URLs that include a field name you might want to restrict it to this character set and length.

TODO: DO I need this valiation now?

## Slugs

The concept of having urls that route to the names of an object in your database is a concept called 'slugs'. Slugs are useful because they're more memorable urls. I'll remember reddit.com/r/funny but it's harder to remember reddit.com/r/551851 which is how default routing works in Rails. 

## Adding Slugs 

Using the gem 'friendly_id' we can generate slugs and create them.

1. You'll need to add the gem to your Gemfile and install it.
2. You don't need to generate a new field or do anything like that. We are just going to already using our existing name field and modify it so that it becomes a friendly id. 

This should magically work now!

You should be able to go to localhost:3000/subreddits/name_of_subreddit.

## Adding Resource matching

There's some additional work in changing it to be /r/name_of_subreddit so we'll keep that off for now. If you want to add that you can look into route matching itself. 

I can give you a hint that you would need to add a route to routes.rb that points to the appropriate show action for the resource you want. 

## Adding Moderators

You should now work on adding your first migration that allows you to add onto the sub reddit object and add the concept of a moderator. 