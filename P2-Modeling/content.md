## Specifications on Reddit what you will be building.

We'll start by building the simplest functionality of Reddit to make it usable for this project. That includes user accounts, subreddits, posting, comments and voting. There will be some more advanced features later but let's narrow it down to this for now.

The first thing when developing a project is to figure out your use cases. We can express what functionality we're building using a few statements. 

This concept is called *user stories* in which we detail the who, what and why we're building each our of features.

Generally the format of a user stories goes along:

```
  As a <role>, I want <feature> so that <reason>.
```

Take this time to think of your own user stories. How do you think it's best to express the features you're building on reddit?

Here are some provided ones:
- As a user, I want to be able to sign up and login into my account.
- As a user, I want to be able to post links to share content
- As a user, I want to create subreddits to create community around topics.
- As a user, I want to be comment and reply to comment on posts that others have put up.
- As a user, I want to vote up/down any post in order to voice my approval or disapproval

Now that you have your user stories. We should figure out how to represent these things in our models. Generally, our **nouns** will be our new models. The relationships between the objects will be more akin to **verbs**. 

## ERD Diagarams

**ERD Diagrams** are a great way to represent the rough outline of your project. In the example below you can see that each piece is a model. It has a name of the model and a few fields that are associated with the model. The example mentions things like Item 1, 2, 3 but it's akin to what properties does that model have. Your users will have at least an email address and a username. 

TODO: Add picture

So given that, what are your models for Reddit? At this stage there should be 5. Draw it out and assign the fields to each model. Describe the relationships between these models based on your user stories.


### Teacher Follow Up ###

Students should be able to think about what they are doing and create some type of ERD Diagram at this point.

The 5 models are going to be:
Users, Subreddits, Posts, Comments, and Voting.

Checking against this the students should have:

1. A user makes a post
2. A post belongs to a subreddit
3. Comments and votes should be tied to a post and a user

If the students are not that at that stage or missing pieces, explain what parts are missing and which user stories did they cover or not. Translating user stories.

TODO: Create a ERD Diagram for reddit