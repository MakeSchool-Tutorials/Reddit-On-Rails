# Section Voting

## Spliting up

If you want, this is another great time to split up. We're going to be covering some topics about voting here while the other section will cover more topics about front-end organization and css. Figure out your partner's strengths and preferences and split up. 

## Voting


One of the biggest things about reddit is the ability to vote! Upvotes, downvotes, leftvotes, green votes! But more importantly we're going to need track of all votes that happen in our system and ensure that nobody has more than one vote on any post. So let's add voting to our model.

What is important in a vote? A **user** has to vote **up** or **down** on a specific **submission**. We can determine what our relationships and our model will look like from there. I'll leave this an exercise for you to figure out and check back on this once you're ready. I'm going to influence your decision here though. Think about what else you vote on reddit? What did we learn last lesson that might be useful.

Take a second to determine what this might look like based on the hints.

## Voting - Models

Votes belong on both posts and comments! So let's create a polymorphic relationship again where vote belong to a "votable" object which can be either a post or a comment in this case. That way we can re-use our voting model for both comments and posts. 

Try to think of what validations you'll need and set up their up at this point. You'll also need a uniqueness constraint on user_id but only based on the votable item. For that we can learn about :scope in a validation, this allows us to specify a uniqueness constraint given another field's unique constraint.  Here's an example:

```
	class HolidayCalendarEvent < ActiveRecord::Base
	  validates_uniqueness_of :name, scope: :year
	end
```

As you can see this allows us to have Christmas every year. Without the scope we would be only allow us to have one Christmas and unless you're a Grinch you don't want that. So the scope requirement us allows to have only one holiday of each type but in a year. 

## Voting and Views

When you vote on something in reddit you increase it's vote. If you downvote you can move a vote into negative values. So the score of any post or comment is in fact the total # of upvotes - the total # of downvotes. We might want to create a quick method on our submission model to help us calculate this quickly so we don't have to do it over and over again and make sure to display this on our view. Add the vote up and down buttons right now and we'll hook them up in the next step.

## Adding Voting

# TODO: Do I divulge into JQuery here and best practices about that or do I teach angular or should I just stick with Rails tools to do work here. 

So the magic of Rails allows us to do quite a bunch of updates without having to do lot extra work. Let's learn about the magic of link_to. A link to generates the URL normally in Rails app but if we specify that this is a remote link, it will retrieve things dynamically using JS for us. Specifying the method post will allow us to send a vote command without having to do any extra work involving JS itself. 

```
<%= link_to "&#9660;".html_safe, votes_path( { upvote: false,
                                       submission_votable_id: votable.id }),
                                       method: :post,
                                       remote: true,
                                       class: voteClasses[1] %>
```

# TODO: How do I fix this for both votes and comments? Adding a comment_votable_id and specific. 

We can add this down vote and upvote ability quickly and easy for all our commands.

# TODO: This section seems sort, maybe we can talk about using Redis to speed up our operations and act as a cache. 