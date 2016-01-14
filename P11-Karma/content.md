# Karma

On Reddit posting isn't altruistic, you get that delicious karma. Karma is pretty basic, it is the # of upvotes of all your submissions minus the # of downvotes of all your submissions. It's a pretty easy calculation so let's build that out first.


## Build Karma

Let's add a method to the user object that calculates a user's Karma and add the ability to see your user name and karma score in the top right of the header. Just go through a user's submission for now and calculate the score. We don't want to store the karma in the user table itself. 

It might be beneficial to have a method on the Submission model that calculates the total # of upvotes to simplify things. 

## Speeding things up

Now that we're showing Karma on every request, it's adding an expensive query to each our request. Take a guess at why this query is so expensive! 

[Solution]
The query goes through a user's submission and for every submission it has to calculate all the votes! That means we're doing that N+1 query issue that we had before. We could do the same solution as last time, if you don't know what I'm talking about talk with your partner and have them explain what's going on.

We can build this out better in an easier way using a **key-value database** called **Redis**. 

Key-Value database is a different type of database than our traditional Postgress, MySQL, and SqlLite. Instead of storing data into a table, you are just making a very large dictionary mapping keys to values. You can store lots of different data structures and more importantly Redis stores the entire dataset in memory. This is significantly different from databases which persist all their data into the disk. 

The upside of Redis and storing things into memory is that it's faster, an order of magnitude faster to retrieve things from memory than disk. The downside though is that you can't necessarily store important information on it because even in the best solutions Redis eventually will persist information to a disk but it has a delay unlike SQL databases. 

So many people use Redis as a cache or a place for information that needs to be retrieved quickly but we don't care that much about losing. In fact, redis keys have a default expirey time. 

## Redis Setup

### Install Redis

This is where brew comes into place. We're going to install Redis on our computer by doing

```
	brew install redis
```

### Run Redis

After it's installed, open up another terminal window and call redis-server. Note which port the server is running on. Mine is on 6379 which is the default 

### Install gems 

Install the gems we're going to need for Redis working with Rails. Add the following gems to your Gemfile:

```
	gem 'redis'
	gem 'redis-namespace'
```

The redis gem is a ruby wrapper around Redis and redis-namespace is a gem for us to utilize Redis with specific namespaces. In the future we might have multiple redis-namespaces, maybe we want to store karma and other reddit related things and another Redis dataset to store some internal tool informations. We don't them all in one big dataset. 

### Configuration Redis

Create a new file called ```redis.rb``` in config/initializers and type in the following

```
	$redis = Redis::Namespace.new("reddit_app", :redis => Redis.new)
```

Once that's up you can load up a Rails console and make sure your redis server is working! 

Try running:

```
	$redis.set("foo", "bar")
	$redis.get("foo")
```

Does that all work?! Awesome! You now have a Redis configuration available to you everywhere in the app using the variable $redis now. 

## Caching Karma

Let's modify our karma method in the user object to use Redis instead of relying on the database. If the value isn't in Redis, then we need to retrieve the value from the database and update the value in Redis so the next time we hit, we can cache it. Make sure this work! Have some karma ahead of time to make sure that it's working.

We're going to be careful about key though, we want the key to be user specific so that people aren't udpating other people's karma. 

## Updating Karma

We have one problem though, if your submissions gets upvote it doesn't update your karma now. It will update as soon as the time expires but that's no good. Thankfully Redis has a a few methods that allow us to atomically increment and decrement a method. 

You can see the [http://redis.io/commands](full list of commands) on Redis but the ones were going to use are going to be ```incr``` and ```decr```. 

Let's modify our upvote and downvote methods to update the submitter's karma each time a vote gets called. This will allow the karma to stay up to date between expirey times but still allow us to cache karma. Be careful though that upvote and downvote calls aren't being called when they aren't relevant. We don't want someone mashing the downvote button and changing a user's karma. 

Also make sure that changing an upvote to a downvote is appropriately affected. 

Try to think of the other scenario where upvotes and downvotes get changed and fix it so the Redis methods get changed appropriately.

[Solution]
When a submission is deleted, the karma accumulated in that post is deleted.


## Other Benefits to Redis

One of the side benefits of this approach to using Redis is that only current users who are actively logging in are cached in Redis and thus our store only gets as big as the # of active users. We could have stored the results into the database, but then we'd have two sources of karma in the database, one which become offsync but permanent in our database. Redis as a temporary cache makes more sense in this purpose because in the end the real karma calculation is always in the database.

## Using Redis for other purposes

You can use Redis for other purposes as well. By default, Rails caches all its object in a file store and stores all session information in a cookie. 

There are some benefits and downsides to storing our sessions in different ways and this post is a great summary of the [https://gist.github.com/jcasimir/1210255](benefits of each approach). You should read over it and change our session store to using Redis. Unlike most other keys, Redis session store cookies will not have an expirey. 

