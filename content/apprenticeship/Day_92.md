---
title: "Day 91 - Why Monoid?"
date: 2018-12-03
tags: [Haskell, Monoids]
draft: false
---

# Why Monoid?

In my last post I was quite technical on **how to Monoid** and what the text book definition of a `Monoid` is. But what is the point of it?
You could just write a function that does the same.

But Monoids are just abstractions of a common pattern which appears often, Monoids allow you to abstract this common pattern into a set implementation so it can be easily used to construct datatypes together. Knowing the monoidic laws allow you to use any monoid safely without the possibility of running into errors.

Monoids exist everywhere but have been abstracted out and given a symbol. But in the same way that the world excepts the monoids `+` and `*` and when we use them we know that, due to the law of associativity, they will yield the same result. You can also **constrain** your own more complex datatypes to act in a certain **predictable** manner, and by having the datatype instantiate the `Monoid` typeclass, you can be assured that only that datatype can be operated on in that certain way. This constraining of datatypes to specific behaviour isn't just limited to Monoidic behaviour but also the reason for all typeclass inheritance.

#### Folding Monoids
For me personally, it made me really understand folding better. Folding is method based off monoids (kinda). If something is a monoid, then it can be folded using `Fold` or `FoldMap`, which uses the monoidic `mempty` as the base case.

**ramble ramble ramble**
