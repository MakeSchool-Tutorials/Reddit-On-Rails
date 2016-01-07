# Comments

## Merging

Before you continue on we should make sure everyone on your team is on the same page. If you spliot up the work we will need to merge our voting code with our home page code. We want to make sure that the partials created in the home page section work with the new code that we needed to add for voting. Take this time to make sure the code for voting gets put into the submission partial properly so we can do votig properly on both the comment page and the home page!


## Starting

Now that we have posts and voting, we need to focus on our next step. Comments, what's the point of reddit without some quick puns and ridiculous memes? Or real discussion (really depends on the subreddit). Either way, we're going to need comments and the first thing that we need to realize that parents can have two types of parents! 

Comments can either belong to other comments as **replies** or comments can be long to a post as a **comment** on that post. 

So let's create our comment model! Let's talk about what features we're going to need for our comments. Thing about what are the necessary attributes of comments and how their relationship is to other objects that you've created including users and submissions. I recommend reviewing over our knowledge of polymorphic inheritance to create a field called 'commentable'.

## Visualizing Comments

So let's focus on our first step in showing comments and posting new comments. We can quickly render each comment as a partial, if you don't remember go back to our quick coverage about how to render partials for each model in the home page section. 

## Creating new comments

After that we can continue with our work on submitting a new comment. We can use a little utility called **form_for** that will help us create a lot of the infrastructure for creating a form to submit a new comment on our submission page. The form_for object though needs an empty comment object in order to work, so we'll have to add some code into our controller to give an empty object to work with. 

```
	@comment = current_user.comments.build 
```

Our build action will automatically populate this comment's foreign key to attach it to the current user for us and now our form can use this comment to submit and create things. Let's add some HTML to our code:

``` 
	<%= form_for @comment do |f| %>

		<%= f.submit "Post", class: "btn btn-primary" %>
	<% end %>
```

This will create an empty form, but form_for isn't magic and we need to populate each field properly. Form for creates a block that allows us to use a variable to create form fields. In the above example we've named this variable f.

We can create labels for fields using ***f.label*** or create a text_area and other types of HTML inputs. You can read more about all the types of fields we can create and their available options [http://api.rubyonrails.org/classes/ActionView/Helpers/FormHelper.html](here). We'll need a text area field for our comment content though.

You will need two hidden fields that link this comment to our commentable object as well as the commentable_class, otherwise the form won't know what to to attach the object to. Create two hidden fields called commentable_id and commentable_class and populate them appropriately.

By the end of this you can create comments. Try posting a few comments to our page for now to make sure everything works.

## Nested Comments

Now that we can submit regular comments to our submission, we're going to need to reply to comments as well. Remember that each comment has a **has_many** relationship with other comments so we can access the replies on a a comment easily by accessing ```comment.comments```.

You can render each reply using the same partial. This will create nested comments! But to explain what's happening in the SQL though, each comment is doing a separate query to the database to get each set of replies. This is called ***N+1 queries problem***, you are retrieving all N comments using 1 query but retrieving all associations of each of those N queries executing N+1 queries. 

This is going to get real ugly fast. So let's do some optimizations. To fully optmize reddit comment trees it's a bit out of scope of this tutorial so let's try to reduce what we need to do by only allowing replies on the first level of comments. Modify your partials so that we only render replies on our first page but not on any subsequent comment. We can pass in a variable into the partial like we did before to determine wether or not to render repiles.

But the fundamental problem still exists. We're still doing N+1 queries! Rails thankfully has a wayt o help us avoid this called ***eager loading***. When you generate a query, Rails eager loading retrieves all the comments and the associations you specified in one database request. So instead of making N+1 operaitons you're making one operation. 

All we need to do is modify your comments query in your controller to use the include statement below:

```
	comments.includes(:comments)
```

Now when you access each comment, Rails already has the information without having to do a query to retrieve the information for you. 

## Bonus: Better associations

```commment.comments``` is a terrible way of describing. If you're feeling up for it read this [http://stackoverflow.com/questions/1163032/rails-has-many-with-alias-name](Stack Overflow post) and see about changing it so that you can do ```comment.replies``` instead. 

## Bonus: Sorting

We want to make sure our comments are sorted by the most recent first. Using the Active Record order command sort by the created_at date. 

If you're feeling ambitious, you should able to implement reddit's other sort options by reading more about them here. The code is in python but it is a very clear blog post explaining the algorithim.

[https://medium.com/hacking-and-gonzo/how-reddit-ranking-algorithms-work-ef111e33d0d9#.rcilff9c5](Implementing Reddit Sorting)

You can use that same order statement to sort by any function that you specified. It will just do the appropriate queries to get the information. You'll need to be careful about eager loading to make sure that you have the up and down votes. 