# Authentication

## Teacher Steps 

Make sure that students have merged their user model into the development branch, that both pairs have run migrations. They should be able to create a user object and delete a user object.

## Making sure everyone is on the same page.

This is the point where if you wanted to split off your work you should be able to have one partner work on authentication and the other working on subreddits! 

Make sure that all your environments are setup to be the same and everyone has the same migrations. We'll create a new feature branch for this section called 'authentication'.


## Validation

The first thing before we do authentication is to make sure we have validation on the user objects set up. If you haven't already reviewed over the materials at RailsTutorial.org it will walk you through how to do validation on your user objects to ensure emails and user names are correct. 

[https://www.railstutorial.org/book/modeling_users#sec-user_validations](Validation Instructions)

Remember to always write your tests cases first to make sure that you know exactly what you're testing for. 

## Secure Passwords

Also finish the section about adding a secure password to your user model. 

[https://www.railstutorial.org/book/modeling_users#sec-adding_a_secure_password](Adding a secure password)

TODO: If I teach rspec will this not work for them?

## Signup

You should able to create authenticated users by now and ensure, but we still need to allow sign up and login. The RailsTutorial goes through this step by step as well helping us make the process easier for you. We won't be doing profile images so if there is any mention of Gravatar or images don't worry about it for now. 

Let's go through and add the appropriate routes for signup first.

Modify your routes file to include the signup page

```
	Rails.application.routes.draw do
	  get 'signup'  => 'users#new'
	  resources :users
	end
```

We can now follow the instructions at RailsTutorial about creating a sign up page. We'll be using the form_for which is a useful tool in building forms for any type of submission. Work on this until you hit the section about Proessional-grade deployment.

[https://www.railstutorial.org/book/sign_up#sec-signup_form](Sign up form instructions)

We won't be workingon the production server components just yet so let's not worry about adding SSL. 

## Login

The major thing about reddit is that you have authenticated users, so we now need to ensure that any user actions such as voting and other stuff needs to be done by a logged in user. We'll be learning about sessions

**Sessions** are the concept that once you have logged in, the server will use somet type of cookie in your browser to tell the server that you've logged in. This allows you to know which user is doing the action as well as knowing that an authenticated user is doing the action. This prevents random visitors from doing certain actions on your site. 

Let's build login pages do all the sections available at RailsTutorial about building login and logout. You can ignore any specific changes to the layout unless you deem it appropriate to add something. Perhaps adding a profile link to your header.

[https://www.railstutorial.org/book/log_in_log_out](Login Instructions)

## Facebook Login TODO: This requires server side code and a real url that they can point to for the Auth Calback right?

Check with your partner. How are they progressing on their project? Are they way ahead of you? If they're done with their part of the project let's merge what we have now so that they can integrate their portion. They should be able to add authentication to their app and make sure your both on the same page. 

If you're ahead and your partner is still behind on subreddit creation, just continue on and build Facebook login.

Let's add Facebook signup and login to our proccess. If you don't have a Facebook account you should create one now. 

I recommend using the gem 'omniauth-Facebook'. Which is a great industry standard gem that allows you to quickly add Facebook authentication to your project.

### Steps

TODO: This sucks because we need to have a server side callback, it won't work without that since Facebook's callback won't hit our local server. Maybe explain gem proxy local instead of going into heroku and all that fun stuff?

1. Create a Facebook app 
TODO: Go back to this. You'll need two important pieces of information here. You'll need to remember the key and secret here and store that someplace safe. 

2. Store that information someplace in your environment (TODO: Adding environment variables) and make sure to note what it is, we don't want the credentials in our codebase otherwise people could use our secret key and token for malicious attacks if they found our code. For now we're going to just store in our settings since it will won't doo too much. TODO: how do I solve this? Environment variables are annoying when working with others.  

3. You can find instructions for the gem available on it's [https://github.com/mkdynamic/omniauth-facebook](Github Page). You'll note for Facebook login we'll need to still need to create some type of user name and because of our validations we will need their email addresses. So please make sure to look up how to ask for the email permission Facebook.

3. The more detailed instructions for integrating the OmniAuth application will available here: https://github.com/intridea/omniauth




