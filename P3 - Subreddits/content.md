03 - Subreddits

# Adding some features

We created the Subreddit object in p2: Modelling.  Next, we need need to create the appropriate user stories, tests, and logic for the object.

Some stories to start with are:

* *As a user, I can post content to a subreddits (many-to-one).*

* *As a user, I can edit posts I’ve added to a subreddit.*

* *As a user, I can delete posts I’ve added to a subreddit.*

**T****ask: Add additional user stories around subreddits.  Run these by your teammates, and then write test cases that will fulfill your feature set.  Green your tests by building out the stories you agreed to add.**

# Validations

We're going to need validate a few things for our subreddits though before we continue on. We should review about Rails Validations here on this page: [http://guides.rubyonrails.org/active_record_validations.html](http://guides.rubyonrails.org/active_record_validations.html)

We're going to add uniqueness constraint to our subreddit name to ensure that people don't create multiple subreddits with the same name.

**Task: Ensure that every subreddit is named with a ****maximum_length**** of 21 characters, and doesn’t contain any special characters****.**

**Task: Ensure that subreddit names are unique.**

# Slugs

You'll notice on reddit that the URL for a subreddit is something like [https://www.reddit.com/r/funny](https://www.reddit.com/r/funny), where the name of the subreddit is in the URL. The concept of having urls that route to the names of an object is a pattern called slugging. Slugs are useful because they allow us to create more memorable urls. I'll remember reddit.com/r/funny but it's harder to remember reddit.com/r/551851, Which is what Rails routing would do by default.

**Task: Write a user story that captures slugs.**

**Task: TDD slugs, and use Capybara to ensure that you reach the correct subreddit using the ID or the slug.**

## Adding the slug

Let's create a new field in our subreddit model called slugs. It should be a string with additional validations over our names. Don't allow the slug to have any whitespace or include slash characters.

**Task: Add a slug field to Subreddit, following TDD.**

**Task: Validate the slug to prevent whitespace, slashes, ensure uniqueness, and prevent other special characters.**

## Create a method that creates the slug in our model

We're going to need a method that translates the name into a slug. So let's create a method that strips all illegal characters from the name so that our application can create a slug. Add this method to the Subreddit model.

But we also don't want the user to have to type in a slug, we just want the slug to be automatically there when we create or modify a subreddit. The subreddit should automatically generate its slug before it saves.

**Task: Use a ****before_****validate on: :create**** hook to automatically create the slug and persist it to the database.**

**Task: Add a validation that all the subreddits have a slug.**

## Routing

Now that we’ve added and validated our slugs, we need to add routes so we can use them.  The first step that we'll do is add our route in the routes.rb. If you look over what we have now we'll see that it's mostly resources. We'll be adding our own matcher. You can read more about routing here: [http://guides.rubyonrails.org/routing.html](https://github.com/MakeSchool-Tutorials/Reddit-On-Rails/blob/master/P6-Subreddits/here).

Next, let's add a route that matches localhost:3000/subreddits/<slug> and send that to Subreddits#show controller action.  If the slug is presented, use it to look up the correct subreddit.  If not, defer to the primary key of the Subreddit.

## Improving performance

One of the downsides of slugs is that it is slower than looking up a subreddit by id. When you visit /subreddit/1 it's pretty fast to look up the subreddit in our database because we are looking it up by primary id. In most modern databases, the primary id is automatically indexed. However most of the time, it won’t matter unless your table is really big. See explanation [here](http://stackoverflow.com/questions/12431107/performance-of-string-comparison-vs-int-join-in-sql).

In reality this query is likely more than fast enough, but stick with me. There are some important things about how databases work we can learn trying to make this query faster.

We’re going to create an index. If you don't know about indices already, they are a database concept in which we ask the database to keep a separate data structure that allows us to search a field quickly. An index adds an additional cost of maintaining the index whenever you create, delete or modify an entry, so we add indexes sparingly. A good rule of thumb is add indexes on things that you will write queries for and never on text fields.

**Task: read more about indices here: **[https://www.dreamhost.com/blog/2013/08/27/mysql-indexing-basics/](https://www.dreamhost.com/blog/2013/08/27/mysql-indexing-basics/)

*Q: How does an index make accessing a database table faster?*

*Q: What kind of lookup would not benefit from an index?*

We're going to add an index to our slug column. Let's create a new migration and use the add_index command.

**Task: using the Rails migration generator, add an index for the slug column on Subreddit.**

If you try to run the migration though you will run into an issue. Indexes can't be added to a column when it has empty columns. We need to backfill the column so that we don’t have an empty slugs. We'll run into this situation many times in production code, sometimes we want to add something new but provide some kind of default code that populates something.

Let's modify our migration file and include some code that goes through all the subreddit objects and generates their slug based on their name. Add this block of code before we create our index then we can add our index without errors. Because of our after save callback we won't have to worry about future models, just our existing ones.

# Testing

Always start development with plan and a test.  Here are some cases you’ll want to make sure you’ve caught:

1. The app throws an error when creating any subreddit with illegal characters

2. The app throws an error when creating a subreddit with the same name

3. The app automatically fills in the slug field after both a create and an update

4. The app should route correctly if there is a subreddit with the proper name 

5. The app should throw a 404 if there is no subreddit with that name

**Task: Add tests for all of the edge-cases listed above.**

