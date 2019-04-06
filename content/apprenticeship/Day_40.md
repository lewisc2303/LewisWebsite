---
title: "Day 40"
date: 2018-10-12
tags: []
draft: false
---

# Back to Haskell :) => Functional Patterns

### Anonymous functions
Anonymous functions are used in Haskell when you don't wish to create a function without naming it. It is used for HOFs and it can be more concise.
It is basically writing functions the same way as lambda calculus:

```
f n = n + 1
f2 x y z = (5x + 3y) - z
```
goes to
```
f = \n -> n + 1
f2 = \x -> \y -> \z -> ((5x + 3y) - z)
```
Note: The `\` represents lambda and brackets are used to indicate that the argument is applied to the whole function.

### Pattern Matching
Is a way of matching values to patterns by dealing with specific cases and executing different code accordingly. The output of the function statement goes down the list of cases in order and if the case matches, executes that case.
```
nums :: Integral a => a -> a
nums x =
    case compare x 0 of
    LT -> -1
    GT -> 1
    EQ -> 0
```
Because the `compare` function was used, which is of datatype `Ordering`, which is a `Sum` data constructor, where only 3 possible cases exist and so pattern matching is perfect. With pattern matching, one must be considerate to not implement partial functions; which is where all cases aren't covered and so when a non-covered case fails to match, it throws an exception. A way to avoid this, is to activate the `:set - Wall` function when compiling your code.

Pattern matching can be particularly useful when used for data constructors, which I shall cover more in my next blog post cause Friday.
