# Rohan Todo

1. Identify any sections that would be good to check upon and provide feedback for the instructors to determine if that progres is being made.
2. Contact Dan K about git flow
3. Write up state of merged documentation flow


# Section - Assignment

## Assignment Creation

## Explanation of Reddit

---

# Section - Organizing Teams

1. Teams of 2
2. Talk about benefits of working in teams with industry standard flows
3. Structure of project with split tracks of Path 1 and 2 or allow them to pair together for entire project.

---

# Section - Modeling

1. Talk about user stories and provide some default ones for Reddit after allowing them to work on it
2. Create ED Diagrams to allow them to model their overall app before they start
3. Teachers should check the ED Diagrams to make sure they have some basic models and relationships set up before we keep going.

---

# Section - Setting up RVM and Rails


Working together to make sure your

1. Github project is setup
2. RVM is setup
3. Setup rails
4. Make sure that you're both synced on gems, etc.
5. Agree on text editor white space agreements.

---

# Section - Users

0. Remember to do your work in feature branches. That way you have clean branches and you won't interfere with others.

1. Create your user models. Should be done together. Migrate your models so you have github on your page.

---

# Section - Authentication (Branch A)

3. Create an authentication workflow. Follow the tutorial at RailsTutorial.org and duplicate that. Alternative: Set up things using Devise? The rails project is already set up using that scheme instead of Devise.

4. Create the signup, login page, logout, and session storage.

5. Bonus: Setting up session store using a database instead.
6. Bonus: Adding Facebook Login. Devise might be useful for that. TODO: Facebook's documentation or gem that does this for you?


---

# Section Subreddits (Branch B)

Once you have the user model. You can have somebody else set up sub reddit.

1. Create subreddit model. Created by a user. Do not enforce that subreddits model MUST have a user.
2. Ensure that sub reddits can have a moderator.
3. Create a sub reddit page so you can view the sub reddit. Explanation of routing. TODO: Slugs?
4. What happens if you a user deletes their account, any created subreddits should still be around! Explanation of relationships involving destroy and etc.

---

# Section User Links

Creating User Links and Self Posts

## Section merging

Making sure that we have the two previous stuffed merge in. Should be able to only have authenticted users create sub reddits

TODO: Present code that would show here's the model for URL Content and here's the model for Self posts. How do we change this. Isolate the learning to polymorphic inheritance. 

1. You need two types of models. One for URL submissions one for self text submissions. How would you go about doing that.
2. Go into a discussion of the the alternatives. You don't want to create two different models.
3. Polymorphic inheritance has the benefit of figuring out which model you're looking at while at the same time saying specific fields to both.
5. Have someone create the page that shows what it looks like and shows the links and self posts.

---

# Section Voting (Branch A)

1. Set up for votes for each user. How do you model this? How do you build it using javascript and endpoints.
2. How do you ensure that AJAX requests have session cookies?
3. Bonus implement best algorithim for reddit or hacker news algorithim.
4. Bonus: compare the two


---

# Section Home Page (Branch B)

1. Have the home page show all the posts from all the sub reddits.
2. This is a good time to set up things so you can view things as partials.
3. Reuse the stuff you did on the user link page on your home page and sub reddit page.
4. Learn about setting up boostrap
5. Spend some time cleaning up your css

---

# Section Comments (Branch A)

## Section Merging home page and voting

1. Create comments, make sure that they can link to their parent
2. Show the HTML representation
3. Advanced: be able to hide and show and collapse comments
4. Super advanced. Implement other sorting options for comments.

---

# Section - Admin Controls (Branch B)

## Section Merging home page and voting

Controlling sub reddits

TODO: Maybe how migrations work and stuff.

1. Add a moderator to table, create a migration that allows a new moderator foreign key in the subreddit table
2. Now allow the owner and moderator to delete, edit, and remove posts

---

# Section - Karma (Branch B)

Calculate a user's karma and show it. Karma is the total upvotes from all their submissions.

---

# Section Using Redis To Cache Scores (Branch A)

## Section merging karma, admin controls and home page.

0. We can talk about how database and joins are kinda slow. 
1. Using Redis to cache scores. Update things using that and persist it down
2. Might be kind of complicated to set up here.
3. Setting up Redis might be complicated?
4. TODO: How do scores get calculated now?
5. Nice to have: Creative way to visualize pre-redis and post-redis version. Simple way to show the performance?

---

# Section Static Asset Pipelines (Branch B)

## Section merging karma, admin controls and home page.

1. Let's build some static asset pipeline so that we can use scss.
2. Simplify your css rules by using scss. Ensure cross browser working
3. Explain scss in the context of using css. 

---

# Section Rails 5 Upgrade

1. Unknown

---

# Section More advanced topics

# Section Responsive

# Section Elastic Search

1. Let's build some search functionality using Elastic Search for to search our posts.
2. Be able to limit a search to only subreddits