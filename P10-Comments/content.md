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

This will create an empty form, but form_for isn't magic and we need to populate each field properly. Form for creates a block that allows us to use a variable to create form fields. We can create labels for fields using ***f.label*** or create text_area and other types of HTML fields. You can read more about all the types of fields we can create and their available options [http://api.rubyonrails.org/classes/ActionView/Helpers/FormHelper.html](here). We'll only need a text area field for our comment. 

You will need two hidden fields though that link this comment to our commentable object as well as the commentable_class, otherwise the form won't know what to to attach the object to. Create two hidden fields called commentable_id and commentable_class and populate them appropriately.

By the end of this you can create comments. Try posting a few few comments to our page for now to make sure everything works.

## Nested Comments

Now that we can submit regular comments to our submission, we're going to need to reply to comments as well. It might be better 



