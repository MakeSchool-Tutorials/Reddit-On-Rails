# Homepage

## Intent

1. Setup your home page through routing
2. Using partials to reuse vie code
3. Learning to use a popular gem for pagination of our home page

## Checking in

This is another great time to split up the work. We're going to be covering some topics about developing your home page with an emphasis on view code and routing. 

## Home Page

### Routing

The first thing we're going to do is create a new route to point to a controller method that shows all the posts from all the subreddits. You can create a method main in the subreddits controller. 
 
The root path is a special parameter in routing that allows you to specify it.

``` 
	root to: 'pages#main'
	// this points to pages controller main method
```

### Partials

Get the controller method to retrieve all posts for now without specifying any subreddit type. But we need to render the our submissions! We don't want to duplicate our code again so if you weren't already rendering things in partials this is the time to switch over to it. 

Partials in Rails allow you to reuse views in a quick way. To render a partial you should just specify the path and any ojects that get passed into it. 

```
	<%= render :partial => 'things/thing', :object => @thing %>
```

This allows the partial to access the variable specified at @thing as a new variable object inside of it. You can now write your partial to use a common variable that you can pass into it from different spots in your code. 

To create a new partial, we just need to create a file with a underscore in the beginning, which is the convention Rails uses to indicate a partial vs a regular view. Let's try to create _submission partial that we can reuse in multiple parts of the site.

Setup the home page so that we can use this partial to render our submissions on both pages now.

### Pagination

We're not at stage that allows us to render partials and home page but the home page can now have a lot more listings and will become a lot bigger than the other subreddit pages. We need to paginate our posts so that we can show multiple pages of content. 

We'll integrate our first gem in order to develop paginated posts. 

[https://github.com/mislav/will_paginate](Will Paginate)

Switch over the home page to use pagination.

### Bootstrap

If you haven't already set it up. This would be a good time to start including boostrap css into your home page. 

