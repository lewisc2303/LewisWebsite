---
title: "Day 98 - ToDo List ft. Functor/Applicative"
date: 2018-12-10
tags: [Haskell, Testing]
draft: false
---

# Functors and Applicatives

On Sunday I watched a few videos and read a few documents about the functor and applicative typeclass and the methods they contain. Which is not my usual approach, I have been reading chapter by chapter, the Haskell book and doing exercises as I go along, but a few weeks back I realised that it's not making me apply my Haskell knowledge to real world scenarios. And so I started a Haskell project which was a "To-Do List". But I got stuck on a few things, mainly not being able to correctly, operate on my `Maybe [ToDoItem]` with `ToDoItem` being the datatype created to store information about a To-Do Task.

However by applying functor and applicative to my `Maybe [ToDoItem]` I am able to operate on the list with ease and use the `Maybe` wrap for it's actual purpose, which is to case match for errors.  

Basically functors and applicative methods allow you to apply functions and map over datatypes, which is needed to handle the `Maybe` datatype correctly. Beforehand I was having issues, and trying to remove the `Maybe` wrapper, but now I can use functors and applicative to operate within them.

This lightbulb moment enabled me to complete my Haskell project!!!

The finished product is a Haskell "To-Do list" app which allows you to add, delete and view items that are externally stored in a JSON file. This project has made me understand the use of types and explore the aeson library, which made me understand data de/serialisation and made me trial out different Haskell approaches. At first I stored the data externally in a `.txt` file, but `JSON` is a lot easier to parse.

The project can be found on my [github](https://github.com/lewisc2303/MyToDoTask)

NEXT: How to test the IO functions in my application and clean up the code and remove some work-arounds.

# Usability Testing

Today I also watched a usability test with a couple of the apprentices. This is where a member of the UX team shadows a user using the website and receiving user feedback by asking the user questions about their experience. To be honest this was fairly boring to watch, but insightful to see how UX understand the perspective of the user.
