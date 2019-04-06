---
title: "Day 17"
date: 2018-09-19
tags: []
draft: false
---

# Day 17

### Functional Programming

I have been reading and doing exercises from:

> "Functional Programming in Scala" - Paul Chiusano

Today I wrote and tested 2 programmes in FP without the help of the internet or hints.

One tail recursion function that outputs a fibonacci number when inputted the sequence number as the argument. And the other a polymorphic higher order function (HOF) which recreated the isSorted function.

It was really rewarding when I did it, but in the process I was pulling my hair out. Going through and planning HOFs and recursion in your head, I liken it to loops on a rollercoaster: Going in and out of functions, ending up here, going back there... * I'm rambling *

Whilst going through the book I have tried my best to understand key terms. So I thought I'd write them here to test my understanding but writing them now has made me understand that I don't really understand them enough.

*Pure functions* - A function that has no side effects (no mutation of variable) and returns the same output when the same argument is inputted.

*Referential transparency* - I don't fully get this one. I think if a function is pure, it is said to be referentially transparent ???

*Substitution model* - I don't get this one either. It's something to do with substituting arguments into a function and evaluating the result. And with FP, it's easier to do as there are no state changes?

*Tail recursion* - A type of recursion that is performed to prevent stack overflow. It allows you to store memory in a accumulator parameter. Can be used for immutable for loops.

*Polymorphic functions* - A function that can input any type. Which is helpful when inputting HOFs

#### TL;DR: Functional Programming is hard but rewarding.
