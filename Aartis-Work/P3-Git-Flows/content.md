---
title: Git Flows
slug: git-flows
---

When we use Git on solo projects, we are merely using it as a version control system. It's important to understand the distributed aspects of git when working in a team.



### As a solo user

git init .
git add .
git commit -m "test"
git push origin master ( github )
git push heroku master ( deploy )

Branching for features
git checkout -b 
git merge master

Another thing
git stash
git pop


### Multiple users 

Figure out a worflow that works for the whole team.

- Basics of merging, branching, rebasing 
explain commands here

Tools 


a. Push to Master, But always rebase to keep history intact and reduce conflicts 
origin/master
b. Push to Feature Branch & Pull Request 
feature branch - merge and push
c. Open source projects: Fork workflow ( github is a Git workflow histing service)
d. pushed to a development branch use git-flow extension

milestone
https://www.atlassian.com/git/tutorials/comparing-workflows

You are going to have a single git repo on this project. As a team you need to figure out a workflow

Collaborating on projects 

comparing workflows, git desktop


1. Feature branch, merge and push
2. work on master rebase and push , git rebase less conflicts

1. Fork workflow pattern -> Git workflow hosting service


### Resolving code conflicts

Resolving code conflicts

stash , rebase merge, cherry pick
- When migrations go bad, schema version conflict


- submitting a pull request, test should pass
- branching, merging

- git log
- git hooks


### Tools

Git Desktop
Git Tower

[1]: https://www.atlassian.com/git/tutorials/merging-vs-rebasing 
[2]: http://www.toptal.com/git/git-workflows-for-pros-a-good-git-guide
[3]: http://stackoverflow.com/questions/7614215/managing-conflict-in-schema-rb-created-by-git-operation
[4]: http://jordanhollinger.com/2014/07/30/rails-migration-etiquette/
[5]: http://www.slideshare.net/mariam_hakobyan/git-rebase-merge-32586108