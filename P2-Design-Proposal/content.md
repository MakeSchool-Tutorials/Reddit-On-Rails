---
title: Design Proposal
slug: design-proposal
---

Each team should prepare a design proposal in Keynote. Each member of the team should already be familiar with the basics of Rails and have built a few toy applications. The design should be somewhat in-depth. Include diagrams such as use cases or wireframes to convey your ideas. 

Here are some tips to help you with the design

1. First, come up with a list of use cases.
2. Dive into a few use cases and design some initial page flows. 
3. Discover and define the models. Domain Driven design, rough rule is nouns become models, verbs become methods

4. Define the relationships between models, one-to-one, many-to-many, one-to-many and so on.
5. Research [Ruby Gems](https://rubygems.org/) you may need and list alternatives. Think about the Pros and Cons of using a particular gem. Is there a service available through the Cloud provider such as [Heroku](https://www.heroku.com/). Can you use that instead of a Ruby Gem.    
6. Look at common features or cross-cutting concerns across the whole app.
    How will an administrator manage the app?
    How will media be handled/stored?
    Will the app be internationalized?
    How will mail be handled?
7. Prepare a timeline and estimate for each milestone. 
8. Decide which DB you will use
9. Deployment: Heroku is easiest, but this is a good time to explore other Cloud services and their offerings.
10. UI, Pick a CSS Framework such as [Bootstrap](http://getbootstrap.com/) or [Foundation](http://foundation.zurb.com/).
11. Testing - Decide on Integration and/or Unit tests and the testing frameworks to use.

You can use any of the commonly used Design/Diagramming techniques. Don't feel that you have to make the design perfect, However, it is important that you have **some details figured out** before you start. Hand drawn page flows work just as fine. It's the code that matters.

Below are some examples to give you a starting point for designing. The examples are generic and not realted to Reddit.

### ERD diagram

An entity-relationship diagram (ERD) shows the relationship between people, objects, places, concepts or events within that system. Think **Nouns**. 

![](ERD.png?raw=true)

### Wireframes

A Wireframe, which is a layout of your site or page, can help you decide on how to allocate space.

![](Hulu_Wireframe_Sample.png?raw=true)

### Use case diagrams

Use case diagrams shows how users interact with the system.

![](UseCase.png?raw=true)




 

