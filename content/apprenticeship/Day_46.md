---
title: "Day 46 - Referential Transparency"
date: 2018-10-18
tags: [Haskell, Referential Transparency]
draft: false
---

# Referential Transparency

Whilst going through some recursion exercises in Haskell, I thought to myself, how is the recursive parameter in a recursive function not mutating? Surely this variable is changing with with every recursive call and therefore breaking referential transparency?

So, I decided to write a blog post about it...

First of all, what is Referential Transparency?

>Referential transparency is an expression that can be replaced with its value without changing the program’s behaviour.

And in Haskell, functions are considered expressions so, given the same arguments, they must be able to reduce to the the same result every time the function is called.

However back to the original dilemma, when implementing recursion, you often use a **"mutating"** parameter which changes with every recursion call...

And mutability of an expression violates referential transparency.

### The problem

To further understand, lets breakdown a recursive function I did a couple days ago.

```
multiply :: Integral a => a -> a -> a
multiply n1 n2 = go n1 n2 0
 where go n1 n2 count
        | (n1 == 0) = count
        | otherwise = go (n1 - 1) n2 (count + n2)  
```
The parameter in question is `count` but more specifically `count + n2`. Every time the `go` function gets called, a new value is entered into `count`.

### My understanding

However when evaluating (not going to write it out because it would take me ages) I realised that count isn't a value that is mutating, count is merely a binding. Analogous to the `x` in `\x -> x +1` . And the argument value being inputted is `0` and this does not change, but just goes through successive `+n2` operations and the results get saved temporarily in a stack. So count was never an expression so doesn't break RF.

**This is just my ramblings and understanding of it, so if there is an FP inclined person reading this, please leave a comment and correct where I may be a bit misguided.**
