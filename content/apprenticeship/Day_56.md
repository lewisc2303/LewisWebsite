---
title: "Day 56 - Lists"
date: 2018-10-30
tags: [Haskell, FP, Lists]
draft: false
---

# [Lists]

Okay, I did the list chapter from the Haskell book before Innodays, however I never did a blog post on it. And in this chapter there was some crucial information on the idiomatic ways Haskell deals with lists, so I am reviewing what I learnt and writing a post about it...

### The cons (:) operator

One of these idiomatic Haskellism is the cons operator `:`. Haskell has 2 ways of defining the List datatype:

```
data [] a = [] | a : [a]
```

The first is straightforward however the second is a recursive `head` : `tail` syntax.

This syntax is syntactic sugar for pattern matching and recursions.

e.g.
```
capitaliseAll :: String -> String
capitaliseAll [] = []
capitaliseAll (x:xs) = toUpper x : capitaliseAll xs
```

### List Comprehension

List comprehension is a way of generating a list from a list.

On the **left hand-side** of the pipe `|` you have the output function that applies to every element in the list.

And on the **right hand-side** you have the input list with the `->` signifying which parameter in the function it applies to.

```
mySqr :: [Integer]                    
mySqr = [ x ^ 2 | x <- [1..5] ]

myCube :: [Integer]
myCube = [ y ^ 3 | y <- [1..5] ]
```
#### Predicates
Predicates are a way of limiting the list generation by adding expressions that evaluate to Boolean, the list will be generated while the expression is `True` and evaluating from the outside in.

e.g.
```
myTuple :: [(Integer, Integer)]
myTuple = [(x, y) | x <- mySqr , y <- myCube, x < 50, y < 50]
```
