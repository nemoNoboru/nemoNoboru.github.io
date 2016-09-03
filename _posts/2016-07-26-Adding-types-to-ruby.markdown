---
layout: post
title:  "Adding a system type to ruby"
date:   2016-07-25 12:33:00
categories: Projects Ruby
tags: Microgems Ruby Types
image: /images/mt.png
time: "3 minutes"
excerpt_separator: <!--more-->
---


> A type system is the most cost effective unit test you’ll ever have.   

*Peter Hallam*    

# monkey tipin' my way to robustness

If types are a good thing , optional types are even better.  
With optional types you can specify the types of things that really matter. No need
to type all the variables and functions on all your code.  


Types is a easy way of saying "this method takes a number, a list and returns a string"
if you send to this method two strings it will return an error because
the method don't is designed to work with two strings. It is supposed to work with a number and a list.  
If the method returns a nil there is an error on the logic of the method. Easy isn't it?

<!--more-->

In Ruby we don't have this behavior. We only can say: "this method take two things, and return something"
This is pretty ambiguous. What if we send 2 lists to the method? from the point of view of ruby that is perfectly
right. You can pass everything to it.  
And what if the method returns a nil? from the point of view of ruby there is no problem. nil is something.  
As a developer you will only view that the method logic is broken when **another** thing breaks because the method returns
something that is incorrect.  


Even when you finish coding and all the codebase runs smoothly you are kind of insecure about your code.  
when the firsts pull requests appear you have to read all the changes and act as a compiler to check if
the correct type of things get passed to the right methods. And this sucks. this sucks soooo much.  


The lack of types in ruby is even worse if you are interfacing with native extensions (wich are written on C/C++ ) you just NEED types. your codebase becomes a suspense horror movie where things can go pretty wrong if you send the wrong parameters.  
with scary-full-screen-stack-trace-big-errors things.      
Of course, I'm just a student so i make a lot of mistakes sending things and get a lot of scary-full-screen-stack-trace-big-errors.  


So, i just written a microgem (70 lines) to add optional types to ruby.  
Is called "monkey_type" and you can check it out [here][monkey_link] or in [rubygems][rubygems_link]

[monkey_link]: https://github.com/nemoNoboru/monkey_type
[rubygems_link]: https://rubygems.org/gems/monkey_type
