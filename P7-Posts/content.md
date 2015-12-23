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

So what are the downsides of this?
1. You now have a clustered data model. Right now each type of post has at least one empty column. If we start adding features to each URL posts or Link posts you now have keep adding empty columns to either one. What if we add a new type of post? We're going to get more and more column and the data will diverge more.

2. You now have to check the type each time you're using it. This creates overhead and if you forget to do it you might end up going over a large table.

## Polymorphic Inheritance

So we know having one giant table is no good but we also don't want to have duplicate a bunch of information for both tables either. That would require duplicating code and that goes against DRY principles in Rails.

Rails thankfully has Polymorphic Inheritance!

We'll create a class structure in which we have a base class (Submission) with their own subclasses (LinkSubmission) and (TextSubmission). Any fields common to both will belong in Submission and any specific logic will belong in the respective subclass. The database structure will also reflect this and