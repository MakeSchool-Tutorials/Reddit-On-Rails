# Creating the User Model

## Teacher check-in

1. There should be a git repo that both students are on and using on their respective computers
2. They should be able to run Rails server without any issues on each of their computers.

## Starting

So let's build out some real code. We're going to generate the basics for our user model. Before you start touching a bunch of code though let's make sure that we are using best practices for multi-person development.

Review over git flow if you haven't already, but if you have let's create a new feature branch called **user-model**. 

So run the command:

```
	git flow feature start user-model
```

This should move you to a new branch called feature/user-model

You can always check this by running ``` git status ``` in your terminal. If you're using the Github app, it should indicate that branch in the top left. (TODO: Add picture?)

TODO: Should I figure out what they're using for git? 

Now that we're in another branch, we can make changes, commits, and push our changes to the server without affecting any other developers working on this project. We haven't split up yet but this is useful so you can make incremental changes in your project without affecting others. Another benefit of feature branches is that when we want to include the feature into the master branch it's titled by one nice merge commit so our git history looks nicer. 

## User Models

Let's get back to our user model. What fields do we need for a user? If you put down what columns you need already in the ERD Diagram, great! Otherwise think about the fields you'll need for a user. What identify information do you need for a user? What information do they need?

The following fields are necessary:
 id - Integer
 username - String
 email - String

So let's generate this for us. Rails has a great command that will automatically generate models, controllers, and other resources for any model you want to create. You can read more about the generate command here: http://guides.rubyonrails.org/command_line.html#rails-generate

But for now let's generate our user object. Make sure your in your project directory when running these commands.  Rails will automatically generate us an id for us for any new model unless you specify otherwise. It also generates created_at and updated_at as fields for us automatically for any new model. This will be useful for showing sing up dates or calculating how long someone has been on reddit later. 

```
	rails generate scaffold User name:string email:string
```

You can see the terminal output shows how many things we created: migrations, controllers, models, test classes. It's a lot. But we'll focus on the migration. There should be a new file in your db/migrate folder. Open that and we can read about what this is. 

In this folder we'll see what happens. There's a single class with a change method. This is going to be the command that Rails will run in order to reflect our model in our database. 

It should say something along the lines of

```
	create_table :users do |t|
      t.string :name
      t.string :email

      t.timestamps null: false
    end
```

The create_table command above will create a users table with a name field, a email field, and two timestamps field that cannot be null.

We're going to have to run our migrations now. So let's go back to our project directory and run:

```
	rake db:migrate
```


Try running rails server and going to http://0.0.0.0:3000/users to see what the current users on the system. You can also create, edit, and delete user objects here thanks to Rails scaffolding.

At this point there should have been enough progress where you feel comfortable to create a git commit.

Let's create a commit and explain what we've just done.

At this point you should have made a decent base for people to split off! Make sure that you check in with your teacher to make sure that two of you at a good point and if you choose to you can split the next two modules up! 



