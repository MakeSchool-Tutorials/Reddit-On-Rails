---
title: "The Engineer's Mentality"
slug: the-engineers-mentality
---

# Introduction

We are using [Ruby on Rails](http://rubyonrails.org/) to build a Reddit clone so we can focus on learning how to build a well-architected, stable and scalable web application. This project is presented in a similar fashion as a project spec might be provided to an engineer by an architect.  We’ll focus on a TDD approach to creating an application by writing our failing tests before writing the code to correct them.  We’ll use gems accepted by the open-source community to learn the correct nomenclature for common programming patterns, and will require you to understand the documentation for these tools prior to implementing them.  We’ll also introduce the idea of peer code review and focus on following community-accepted best-practices.

By the end of this tutorial, you will  have accomplished the following:

1. Follow TDD to develop a robust and stable web application.

2. Learn how responsibility is divided between parts of a Rails application.

3. Understand common libraries and nomenclatures used in web applications.

4. Understand and be able to reinforce best-practices through peer code-review.

# Why / What is Reddit?

Reddit is a simple web application that we’ll use to cover many of the concepts that would be required during development of a production-ready application.  Hopefully some of you have heard of or used Reddit before, but if not, you can find info about what reddit is on [wikipedia](https://en.wikipedia.org/wiki/Reddit). The basic premise is you can create posts for other users who upvote or downvote the content which moves the post up or down the front page.  Users can also comment on posts, and comments on comments.  We recommend creating a reddit account, creating a subreddit, creating a post, and commenting on another user’s post.  Play with up and down voting as well, as a basic understanding of these core features will be of importance during this tutorial.

**Task: ****Create a Reddit account**

**Task: Create a subreddit (topic doesn’t matter, but keep it work safe)**

**Task: Create a post in your subreddit**

**Task: Add another student as a moderator to your subreddit**

**Task: Comment on the post you created for your subreddit**

**Task: Attempt to edit and delete a post in your subreddit from another user.**

# Notes on this Tutorial

You will be graded on the quality and coverage of your testing, so be sure to follow TDD and use the tools we’ll introduce in the next lesson to ensure adequate coverage.  Don’t be afraid to ask for guidance, and don’t be discouraged if you’re asked to reimplement aspects of your application due to inadequate testing or poor pattern implementation.  You’ll also be given the opportunity to pair program aspects of the project if that seems valuable to you.  

**Task: watch an expose of live, hilarious pairing here: ****[https://www.youtube.com/watch?v=sn7prRGGp4**Q](https://www.youtube.com/watch?v=sn7prRGGp4Q)

# Learning through doing

Throughout this tutorial you will be learning how to build a project from the ground up in the same way you might build a project in a professional environment. You will be expected to digest documentation and apply it to your project without step-by-step direction from an instructor or the tutorial.  Yes, this will take more time and seem more complex, but you’ll benefit greatly from being developing and guiding your own work cycles.

An important part of performing well on a team is understanding the best practices and style guides implemented by the team.  An excellent place to start is here: [https://github.com/styleguide/ruby](https://github.com/styleguide/ruby). This style guide is widely accepted by the Ruby FOSS community..

**Task: Read and reference the Ruby style guide for all code written for this project.**

All of your work should use strict Test Driven Development (TDD) as covered in the Hartl tutorial and you should be regularly reviewing and critiquing your partner’s work. Be sure to apply the patterns and styles you have learned thus far in the rails curriculum.  Instead of being guided through the steps necessary to build a feature, you’ll be directed at the community-accepted documentation to absorb, understand, and implement.  We’ll be using the SimpleCov gem to help you ensure adequate test coverage.

Approach this project as if you were delivering it to real customers.  We’ll craft user stories (a style of describing a feature ask), and spend time reflecting on our application from the perspective of our users.

# Why Reddit?

Reddit presents several interesting problems for us to solve together. There are complex database relations between users, their posts, and the subreddits those posts belong to. Possibly the biggest benefit of modeling reddit for this tutorial is that it provides a set of problems that must be solved in order to build something like reddit, but provides a number of points where you will be able to expand the base feature set as you see fit. This tutorial will focus primarily on getting you from rails new to Reddit, but feel free to talk to your instructor about extending the application in other directions. There are far more things that can be done with a site like Reddit that we will not cover in this tutorial, and those ideas should be explored.  

## Supplemental Materials

Ruby is a very pragmatic language, and design standards have been constructed on the shoulders of giants. Digesting the following resources will both greatly improve your Ruby prowess in addition to giving you a much better understanding of how software is architected and maintained.  All of these resources provide best-practices that are applicable to most object-oriented languages and open source codebases.

**Task: Digest the following resources before continuing:**

* [Community Ruby style guide](https://github.com/styleguide/ruby)

* [The Pragmatic Programmer](https://pragprog.com/the-pragmatic-programmer/extracts/tips)

* [Practical Object Oriented design in Ruby](http://www.poodr.com/)

