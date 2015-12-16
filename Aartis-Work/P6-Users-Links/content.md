---
title: UI-Users-Links
slug: ui-users-links
---

### Spruce up the UI

Users can login and create subreddits, but your UI may be looking bland. Add some styling, this maybe a good time to add a CSS framework in your app if you haven't already done so.

### Usecases for Links

Add usecases for links, Users can create links. How are links related to subreddits, should you change something there


Users -- profile list of posts
Links -- displayed on homepage, sorted by creation time (no subreddits)


### Links and Scoring them

What does the home page show? How does it calculate which submission to show?

How often should scores be calculated and when does the calculation happen, everytime someone submits , every hour etc.


### DB Migrations 

Are the user and subreddit tables changing? 

Pro Tip: don't use migrations in the beginning but simply add/remove column in table, then run
`rake db:drop db:create db: migrate` to start over 


### Users as Moderators

Fine grained Access control


### Refactor 

- consolidate views, scaffolds generates a lot of extra stuff. 
- shared views

Helpers are methods you can define in the files in app/helpers, and they’re made available in your views. Helpers are for extracting the logic from the views; views should just be about displaying information. Every controller that comes from the controller generator has a corresponding helper, and another helper module exists for the entire application:
