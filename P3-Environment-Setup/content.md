# Setting up the Development Environment

## Homebrew
Homebrew is a binary package manager for OSX, similar to APT for Ubuntu based systems, and YUM for Debian based systems.  It allows you to easily install and upgrade command-line software.  Install Homebrew from the command line:

`ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

Once the install is complete, follow the directions given by the installer.  Once complete, close and reopen your terminal to load the new PATH that homebrew has configured for you.  To ensure that all is well, run `brew doctor`.  Stop and get assistance if you receive any errors.

Finally, run `brew update` to update the listing of available packages from the cloud.

## Essential Packages
Before we get started, some essential packages must be installed.  From the command line, issue the following directives:

`brew install git autoconf automake libtool pkg-config apple-gcc42 libyaml readline libxml2 libxslt libksba openssl sqlite postgresql`

This will take a moment, be patient.  Stop and get assistance if you receive any errors.

## Github

1. Create a GitHub account if you haven't already, and login. 
2. Ensure you have access to the `https://github.com/makeschool-17` team on Github, and have one member of your team create a new repository called `RedoR-name1-name2`.
2. One of the members on your team should create a new repository called `reddit-on-rails` or something similar.  There is no standardized naming convention for GitHub projects with the exception that they be named after the project they contain.
3. Add you team member as a collaborator to the project:
	* Navigate to the project's `Settings` -> `Collaborators`
	* Assert that your team member sees the project invitation in their Github interface.
	* Don't attempt to clone this repository yet -- we're getting there!
Note: The repositories do not need to be in the same location on each machine.

## RBENV
Similar to HomeBrew, RBENV is a package manager specifically used to manage Ruby version on your machine.  As you may have noticed, we used ruby to install Homebrew.  OSX (as well as most *nix distributions) comes installed with an older version of Ruby.  We want to ensure we're up to date with the latest and greatest, so the first tool we're going to install using Homebrew is rbenv: `brew install rbenv`.  We also want to be able to automatically install and configure versions of Ruby, so we'll also install ruby-build: `brew install ruby-build`.  

Next, let's get the latest version of Ruby installed: `rbenv install 2.3.0`.  This will take a few minutes.  Stop and get assistance if you receive any errors.

We can check which version of Ruby is being used by the system: `ruby -v`.  You should see that `system` is the current selected version of Ruby.  We want to be using 2.3.0, so let's tell rbenv to set the globally used Ruby: `rbenv global 2.3.0`.  Running `ruby -v` should now show 2.3.0 as the selected version.  Stop and get assistance if you receive any errors.

Lastly, we need to install Bundler, a version manager for Ruby libraries, and Rails:

```
gem install bundler
gem install rails
rbenv rehash
```
The rehash command is necessary only when installing gems without using Bundler (we'll cover this in more detail later) for the first time in a given version of Ruby (each version of Ruby maintains its own set of gems due to version dependency issues).  

## Rails
Rails is an opinionated framework, and comes with a set of generators to make our lives easier.  The first generator we're going to use is `new`, which will create a complete skeleton of a rails project for us.  Only one of the team members needs to perform this step, so please pair for it:

`rails new $PROJECT_NAME` -- replace $PROJECT_NAME with the name used for the repo created under the **Github** section.  Navigate in to your project using the **c**hange **d**irectory command: `cd $PROJECT_NAME`.  Then, using the **l**i**s**t command, check out the directory structure that the generator created for you: `ls -la`.

Next, we need to create a new git repository to store changes and allow you to share the source code of your new project with your team members.  In the directory of your new rails project, run:

TODO: These are incomplete. DANK

```
git init
git add .
git commit -m "Initial commit"
```

## Pushing your project to Github

This step only needs to be performed by the team member that generated the rails project.  Following the directions in the new Github repository created in the **GitHub** section, push the project up.


## Sharing your project with your team members
Now that your source has been pushed to your github, your team members should pull the project down to their local machines using the `clone` command.  This will copy the repository down to the a folder named after the repository in the current working directory.

`git clone $REPO_ADDRESS`

