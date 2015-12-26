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

1. Github project
2. RVM is setup
3. Setup rails
5. Agree on text editor white space agreements.

---

# Section - Users

0. Teacher Check In!
1. Talk about creating a new feature branch for this.
2. Use Rails Scaffolding to create user model
3. Git flow merge your feature back in.
4. Sync up

---

# Section - Authentication (Branch A)

0. Make sure that students have merged their user model into the development branch, that both pairs have run migrations.
3. Create an authentication workflow. Follow the tutorial at RailsTutorial.org and duplicate that. Alternative: Set up things using Devise? The rails project is already set up using that scheme instead of Devise.

4. Create the signup, login page, logout, and session storage.

6. Adding Facebook Login using omniauth-facebook gem.
TODO: Do it myself to follow instructions


---

# Section Subreddits (Branch B)

Once you have the user model. You can have somebody else set up sub reddit.

0. Make sure that students have merged their user model into the development branch, that both pairs have run migrations.
1. Create subreddit model. Created by a user.
2. Create a sub reddit page so you can view the sub reddit. Explanation of routing.
3. Creating slugs: talking about models, routes, and migrations.

---

# Section User Links

Creating User Links and Self Posts

## Section merging

Making sure that we have the two previous stuffed merge in. Should be able to only have authenticted users create sub reddits

1. You need two types of models. One for URL submissions one for self text submissions. Explain benefits of polymorphic inheritance vs single table inheritance. 
2. Talk about creating submission objects and the complexities of it.
3. Draw views for subreddit pages and individual pages

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