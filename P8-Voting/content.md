# Voting

## Intent

1. Tracking votes using models
2. Using asynchronous javascript or Rails code to develop voting

## Checking In

This is another great time to split up the project. We're going to be covering some topics about voting here while the other section will cover more topics about front-end view code and css. This section will cover more Rails models. Figure out your partner's strengths and preferences and split up. 

## Voting

One of the biggest things about reddit is the ability to vote! Upvotes, downvotes, leftvotes, green votes! We're going to need track of all votes that happen in our system and ensure that nobody has more than one vote on any post. So let's add voting to our model.

What is important in a vote? A **user** has to vote **up** or **down** on a specific **submission**. We can determine what our relationships and our model will look like from there. I'll leave this an exercise for you to figure out and check back on this once you're ready. I'm going to influence your decision here though. Think about what else you vote on reddit? What did we learn last lesson that might be useful?

Take a second to determine what this might be. 

## Voting - Models

Votes belong on both posts and comments! Let's create a polymorphic relationship again where vote belong to a "votable" object which can be either a post or a comment in this case. That way we can re-use our voting model for both comments and posts. 

Determine the validations you'll need and add them to the model. 

We also want to limit it so that there is only one VOTE per votable object for each user. We can add uniqueness constraints using ```validate_uniqueness_of``` but how do we ensure that it will work for a votable for each user?  For that we can learn about :scope in a validation, this allows us to specify a uniqueness constraint given another field's unique constraint.  Here's an example:

```
	class HolidayCalendarEvent < ActiveRecord::Base
	  validates_uniqueness_of :name, scope: :year
	end
```

As you can see this allows us to have Christmas every year. Without the scope we would only be allowed to have one Christmas and unless you're a Grinch you don't want that. The scope parameter allows us to have only one holiday of each type but in a year. 

Figure out how to do this yourself but before you start this is a good time to add a test case to make sure that our model raises an error if it tries to create two votes for each item from any user. 

## Voting and Views

When you vote on something in Reddit you increase it's vote. If you downvote you can move a vote into negative values. The score of any post or comment is the total # of upvotes - the total # of downvotes. We want to create a method on our submission model to help us calculate this so we don't have to do it over and over again. Let's create that method and use it in our view to display the score of any post. 

## Adding Voting

We have all this voting code but we can't actually have the user up and down vote yet. We need to create our voting buttons and hook them up. Let's try to only add voting to our submission first to make things less complicated. 

The magic of Rails allows us to do asynchronous updates without having to do lot extra work. Let's learn about the magic of ```link_to```. A ```link_to``` generates a URL in Rails to link to a specific resource, it's a nice shortcut to allow us to generate URLs programatically. 

But if we specify that this is a remote link, it will retrieve things dynamically using JS for us. Specifying that the link is POST method will allow us to send a vote command without having to do any extra work involving JS itself!

```
<%= link_to "&#9660;".html_safe, votes_path( { upvote: false,
                                       submission_votable_id: votable.id }),
                                       method: :post,
                                       remote: true %>
```

We need to modify or create our votes controller create method so that when it is given a ```submission_votable_id``` parameter, it creates a submission object and connects it to our vote. 

## Updating the Vote 

But when we upvote, our button needs to dynamically change! We can use helpers to determine which css class to put on our link_to to style it differently. 

Your helper should return a class for upvoted buttons if they have a vote on them and if that vote is an upvote. Same with the downvote. Make it return a css class that you can then add rules for to style the upvote and down vote button.



