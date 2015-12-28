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

## Facebook Login

Check with your partner. How are they progressing on their project? Are they way ahead of you? If they're done with their part of the project let's merge what we have now so that they can integrate their portion. They should be able to add authentication to their app and make sure your both on the same page.

If you're ahead and your partner is still behind on subreddit creation, just continue on and build Facebook login.

Let's add Facebook signup and login to our proccess. If you don't have a Facebook account you should create one now.

I recommend using the gem 'omniauth-Facebook'. Which is a great industry standard gem that allows you to quickly add Facebook authentication to your project.

### Steps

1. Create a Facebook app
You can go to developers.facebook.com and create an app. Just name it something random that you can remember for this project. Ignore the integration steps, we're going to do server side integration.

You'll need the app ID and the App Secret for the next step.

Configure your app's website to be ```http://localhost:3000```

2. Store the Facebook Key and Facebook App secret in your environment variables. **Environment variables** are variables that exist in your user's environment on any UNIX based operating system. Since they're set on the computer account itself but can be accessed by code, they're useful for storing sensitive keys like you're Facebook App Id and App Secret which we don't want to check into source code. If you just published your keys in your code, someone could find it and make requests using your app.

We can create and manage our environment variables using a gem called **figaro**.

1. Add it our Gemfile
2. Run bundle install
3. Run ``` figaro install``

This creates an application.yml and modifies git to not include it when you push your code. We can add our facebook secrets here. You'll need to share the application.yml with your partner at a future time otherwise Facebook won't work.

Let's add facebook_app_id and facebook_secret_key to our application.yml

If you open up your's rails console you should be able to test this by accessing

```
  ENV["facebook_app_id"]
```

To make sure it works.

3. Now that we have our environment variables set up and our app keys we can now integrate Facebook by using the Omniauth gem.

Omniauth is a gem that allows us to implement OAuth login. **OAuth** is a protocol that allows us to get a **token** from a third party provider like Twitter, Facebook, or Google. This token can then allow us to make requests to these third parties to access permissions.

Think about the time you've hit a Facebook login. When you tap it, you are sent to the Facebook site to properly login to Facebook. This all happens on Facebook's side of things or inside a popup in your browser. Once they've verified that you've logged in they will redirect you back to the app you tried to connect from to a URL they specified with a token that grants that app permission to access certain information on Facebook. This token has an expiration date and you'll have to request another one after a period of time.

To set up Omniauth we're going to need to first set up a provider from Omniauth.

1. Create a new file called ```omniauth.rb``` in your ```config/initializers``` directory

2. Copy this code:

```

Rails.application.config.middleware.use OmniAuth::Builder do
  provider :facebook, ENV['facebook_app_id'], ENV['facebook_app_secret'],
           :scope => 'email', :display => 'popup'
end

```

3. Add a new route

```
  match '/auth/:provider/callback' => 'sessions#create_facebook'
```

4. Create the controller method in sessions

```
  def create_facebook
    raise request.env["omniauth.auth"].to_yaml
  end
```

You can see what's available in our callback to omniauth by visiting http://localhost:3000/auth/facebook.

Your server should print out the information retrieved by omniauth. It should contain information such as their Facebook ID, email, and a token. Based on the information you've gotten back we can create a user now.

5. But we have a problem now. We need to identify a facebook user coming back to the site. We can't let them just sign up and create a new user everytime so we need to add some fields to our user table to identify Facebook users. So let's create two new fields: provider and UID. Which will store the provider we're using for third party authentication and their user id on that service.

So when we now create our session, we search for our user to see if they already exist otherwise we create a new user. You'll run into a small issue with user creation though we'll talk about in the next step.

6. We have one problem. Facebook users don't have a username or a password! So we need to make sure that we generate them a username. For simplicity's sake we will just make this their name.

We do not want to generate them a random password though, we want to make sure that if a user authenticated using Facebook we allow them to authenticate using Facebook only. Different sites have different policies on this but for Reddit we're going to change our validation on password to only check presence if provider is empty.

We can add a ```:unless``` statement to our validation that ensures that can check provider field to see if it's present?

```
  validates_presence_of :password, :unless => lambda { self.provider.present? }
```

We will also need to turn off has_secure_password unfortunately since it requires a presence of a password.

```
  has_secure_password :validations => false
```

7. Congratulations! You now a fully working Facebook login. The omniauth gem works with many providers so you can easily add more sources of authentication. You can see the full list [https://github.com/intridea/omniauth/wiki/List-of-Strategies](here).