---
title: "Day 84 - Compile Driven Development"
date: 2018-11-26
tags: [Haskell, Kata]
draft: false
---
# Haskell Blog

Today whilst researching Monoids I stumbled across a very informative blog, the best Haskell blog I've come across yet.
The blog is well categorised by level of Haskell competency and explores not only concepts but also the best approaches to learning and using Haskell. It has some cool advanced sections like; AI in Haskell, Haskell Web and Haskell parsing. It also goes into Elm and PureScript AND it's still active!

The blog is quite aptly named for this lovely grey, rainy Monday morning...

[MondayMorningHaskell](https://mmhaskell.com/blog)

### Compiler Driven Development

As mentioned above, this blog discusses the best approaches to get the most out of Haskell, one of which was called [*Compile Driven Development*](https://mmhaskell.com/haskell-brain-4). This approach, is adapted from *Test Driven Development*, which is based around letting the passing of tests, drive how you implement functionality. *Compile Driven Development* is a way of letting the compiler drive your code through the understanding of the type system. The blog, explains that this technique is useful when importing and investigating a new library with library specific types.

"The approach looks like this:

- Define the function you’re implementing, and then stub it out as undefined. (Your code should still compile.)
- Make the smallest progress you can in defining the function so the code still compiles.
- Determine the next piece of code to write, whether it is an undefined value you need to fill in, or a stubbed portion of a constructor for an object.
- Repeat 2-3."

I wish I read this blogpost before implementing the `aeson` JSON parsing library into my ToDo project, as it took me too long to implement certain methods into my code, due to the lack of the understanding of the types I was using. A better approach would be to first, implement the library in its simplest case, using `undefined` to first satisfy the the compiler and only type match, and then build up the code and the understanding.

# Kata

This morning we started using our morning Kata sessions to practice certain methods we would like to improve on. Before, we implemented the kata in any way to pass the tests, and the emphasis was on correct naming and letting the tests drive the implementation. But now that we are fairly good at this we are starting to use Kata to improve on certain methodologies.

This morning we decided to look in to *regular expressions (RegEx)*. The Kata was an easy kata from [CodeWars](https://www.codewars.com); the implementation was to return `True` if the first and last letter of the argument *meal* were the same as the first and last letter of the argument *beast*.

The outcome was that we learnt how to use RegEx for determining the first and last letter but we of course made a silly mistake by hardcoding the first and last letter instead of referring to the first and last letters in the string. it was Monday morning so brain function was at <50%.

But hopefully we can speed through it tomorrow morning!

**Also it turns out my RSS feed did work, but out of no where, as I didn't change anything**
