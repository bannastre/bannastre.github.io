---
layout: post
title: "TDD - Red Green Refactor"
date: 2017-05-14 T10:00:00Z
---

Today felt as though, during the night, someone has opened my brain and created new connections in the 'Ruby-cortex'. As Week One comes to an end, the sense that the structure and syntax of this new language is already becoming second nature. So is the method by which we attack each new problem, whereby we seek first to identify the problem that we are trying to solve before writing a test that will confirm the solution. Only then is any code written. I am of course talking about Test Driven Development.

In my last post I talked about Pair Programming and TDD is another rule of [XP](http://www.extremeprogramming.org/rules/testfirst.html). In TDD we take the starting point of a user story and identify the potential objects and messages. This shapes the Minimum Viable Product (MVP) and leads us to our first Feature test; that the object exists. This test obviously fails immediately and until we create the Class. We have created our first "Red Unit Test" - so called because using the Rspec test framework we see it on the command line  with red colour formatting.

I'm also pretty chuffed this week and I have written my own Feature Test script which integrates the idea of [Behaviour Driven Development (BDD)](https://dannorth.net/introducing-bdd/) These are simpler tests to suggest functionality that should exist in the finished product and help guide the Unit Tests.

That may seem a little simple but as we are writing our tests in plain english, the objects and subsequent methods become more intuitive, even down to the name. Say for example we have a user story that requires a user to land a plane. We would simply look to call ```.land_the_plane``` method on an instance of a ```Plane``` class. It's quite clear what this method does. This is an example of [Duck Typing](https://robots.thoughtbot.com/back-to-basics-polymorphism-and-ruby) (if it looks like a duck and quacks like a duck...). Now we can start to code the solution.

Once the test is passed, the colour formatting changes to Green. This not only looks and feels great but is a signal to commit the changes to Github and look to Refactor what we've done.

On reflection this week, I have found that the Red-Green-Refactor cycle should take around 15-20mins max (handy timings for those Pomodoros!). If writing both the test and the solution takes longer than that it's usually a [code smell](https://sourcemaking.com/refactoring/smells) that signifies either the test is too complicated or the code is wrong. Either way, rewrite the test for a simpler step and start again.
