# Submissions on Reddit

## The Immediate Idea

Look back on your ERD Diagram on Reddit you had posts on there somewhere. But the problem is that there are two types of posts on Reddit. There are URL links and there are things we call **self posts**, which are usually consisting of a big block of text by the user submitting it.

We could represent these in one model and one database so let's see what that would look like.

Submissions
created_at: Date
updated_at: Date
title: String
url: String
text: String
user_id: User (who created it)
subreddit_id: Subreddit (it belongs to)
type: Enum

So what are the downsides of this? You now have a clustered data model. Right now each type of post has at least one empty column. If we start adding features to each URL posts or Link posts you now have keep adding empty columns to either one. What if we add a new type of post? We're going to get more and more column and the data will diverge more.

So having one giant table is no good but we don't want to create two separate tables with lots of duplicate fields either. It would reqiure lots of over head to mantain each table to be the same. Imagine adding a new field to submissions, we would need to add it to each subtype. Do that for each field we add. Plus, this goes against DRY principles in Rails of avoiding duplicate code. 

## Polymorphic Inheritance

Rails thankfully has **Polymorphic Inheritance**!

We'll create a class structure in which we have a base class (Submission) in which we will interact with. This allows us to gather all submissions for us and have two separete classes called LinkSubmission and TextSubmission. Any fields common to both will belong in Submission and any specific fields will belong in the respective class. The database structure will also reflect this with 3 separate tables.

This gives us the benefits of only having to query Submission for all the types of our submission but isolates data into it's own respective classes and models in order to avoid the constantly empty fields. 

## Creating the Migrations

You should be able to create the model using our previous knowledge from creating the subreddit table. If you're the partner who didn't create that make sure to teach your partner how it worked. You'll specifically need to remember how to talk about the references field type (instead of say string, or integer). 

I'll be referring to this new reference and polymorphic relationship as **postable** so I recommend naming your new field that to make it easier on all of us. 

If you want your rails generator to build the new field and generate some code for you. You can read more about it here in the [http://edgeguides.rubyonrails.org/active_record_migrations.html#passing-modifiers](Passing Modifiers) section of the Migration spec. 

We'll also at this time create the new tables for LinkSubmission and TextSubmission. You'll have the pleasure of knowing that they do not need to know about their references properly in the table. Rails will handle all that logic for us as long as you've set up the polymorphic relationship.

## Creating Models

Let's try to create the appropriate models so we can get a feel of how to create it. Because we have two separate models we need to create them separately. 

```
	user = User.create(username: "FakeUsername", password: "fakepassword")
	subreddit = Subreddit.create(name: "FakeSub")
	link = LinkSubmission.create(url: "https://www.google.com/")
	submission = Submission.new(title: "Test Submission", user: user, subreddit: subreddit, postable: link)	
```

## Creating Submissions

Now that we have our models and know how to create new ones let's go about creating the page to create new posts. We should link this form to our submissions since that is all we are doing, creating submissions and based on the choices the user picks in the form we will also create a LinkSubmission or a TextSubmission. 

## Testing Submission

This would be a great time to figure out what parameters you'll need and to start creating some tests for our submission controller to make sure that we are creating both links and self posts correctly. You can verify the creation of the models by ensuring that the link objects are created appropriately. 

```
	def creating_link()
		// login in current user
		controller.params(title: "Test Test", subreddit_id: @subreddit.id, url: "https://www.google.com/")
		@link.should_be_created
		// TODO: More information about how to verify that this works right. Rspec is great? Old code base might have some information.
	end

```

You should write a few more tests to ensure that have it work. 
TODO: Change LinkSubmission and TextSubmission into Link And SelfPostable perhaps
