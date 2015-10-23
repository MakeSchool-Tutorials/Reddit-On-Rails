---
title: UI-Users-Links
slug: ui-users-links
---

### Spruce up the UI

Users can login and create subreddits, but our UI looks bland. 

### Usecases for Links

Add usecases for links, Users can create links. How are links related to subreddits, should you change something there


Users -- profile list of posts
Links -- displayed on homepage, sorted by creation time (no subreddits)


### DB Migrations 

Are the user and subreddit tables changing? 

Pro Tip: don't use migrations in the beginning but simply add/remove column in table, then run
`rake db:drop db:create db: migrate` to start over 