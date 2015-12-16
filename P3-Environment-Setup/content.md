# Setting up RVM and Rails

## Github

In case you haven't already set up a github project for your project, we should do that now. Create your user accounts on Github and create a new repository. One of you should be able to create that repository and follow the instructions on the Github site to set up a folder in your project to pull that project. 

In Settings -> Collaborators you can add people who can be collaborators on the project with you. Make sure your partner is a collaborator and that they have pulled the project into their working environment. 

You should both have a folder on your computer now that is linked to the repository. One of you should commit and push something to the repo and make sure the other one that pull those changes appropriately. 

TODO: Do I need to provide more detailed instructions here or should git be familiar enough for students? Refresher might be useful. 

## RVM

Now that you both have a shared repo to work on let's make sure that we can set up our environment the same. **RVM** is an awesome tool that allows you to use different versions of ruby an different gems on a per project basis. This allows you to work on MULTIPLE projects with different dependencies all on the same machine. It also allows a team of developers to have a consistent environment to work in.

You can run the following command to run RVM

```
	\curl -sSL https://get.rvm.io | bash -s stable --ruby
```

Which should install the latest stable version of RVM. Restart your terminal to make sure that it's installed. You can verify that it works by running 

```
	type rvm | head -n 1
```

which should output that 'rvm is a function'.

We'll now create two files in your project. Create a file called **.ruby-version** and write in the line ruby-2.2.3 in it. 

This hidden file ensures that when RVM loads a directory it knows which version of ruby to use. This ensures that we all have the same ruby version and that RVM will install any gems in a local directory as opposed to the global directory.

## Setting up your Rails Project

In case you haven't already read the instructions on creating a new Rails project and setting up your gems, this would be a good time to cover that in the RailsTutorial.org

https://www.railstutorial.org/book/_single-page#sec-installing_rails

Follow the instructions on setting up a new Rails Project though I would name the project a more descriptive name than hello_project. Perhaps something like reddit_on_rails.

You can stop once you hit section 1.3.3. That should be a basic project at this point. 

## Configuring Editors

Make sure that you both have editors set to the same preferences. Tabs vs spaces is a surefire way to make sure that you have conflicts when editing the same file. The general preference for ruby projects is to have two **spaces** without any hard tabs. 

If you're using Sublime it's pretty easy to configure your project to use two spaces.

Go to the bottom right Sublime and choose from Plain Text (or whatever it says) to Ruby.


Settings (Or Subling Text in the top left on a Mac) 
-> Preferences 
-> Settings - More 
-> Syntax Specifix - User

This should open a new file where you can copy and paste the following lines:

```
	{
	  "tab_size": 2,
	  "translate_tabs_to_spaces": true
	}
```

Don't fear if you're using two different editors. You can look up the specific instructions if you're not using Sublime to configure it to use 2 spaces instead of tabs. 