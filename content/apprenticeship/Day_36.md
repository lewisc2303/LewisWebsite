---
title: "Day 36"
date: 2018-10-08
tags: []
draft: False
---

# (More) Types

### Polymorphism

Degrees of polymorphism are:

- Parametric Polymorphism - full polymorphism of any type: `a -> b -> a`
- Constrained Polymorphism - polymorphism constrained to a typeclass: `(Num a, Ord a) => a`
- Concrete type - not polymorphic: `[Char] -> Char`

It is beneficial to keep a function as polymorphic as possible, as it saves you from creating different functions for different types.

But as soon as you apply a function belonging to a typeclass you constrain the argument to the typeclass making it a constrained polymorphic function. This is often necessary as certain functions are only applicable to a certain typeclass and then even more functions are applicable to specific data types; so the more specified you make the type, the greater access to functions you have.

### Typeclass-constrained type variables

Certain functions are constrained to certain typeclasses, sub classes and types; analogous to a tree of compatibility. Functions from the stem can be applied to the branches but not the other way round.

e.g. Take the function:
```
divideLength = 6 / length [1, 2, 3]
```
This does not compile because `/` is of type `fractional` and is an infixr operator and so applies to the right but `length` is of type `Integer` which is not compatible. You would either have to use functions of the same type...

**Or** you can convert `length` to the parent typeclass `Num` by using the `fromIntegral`. And so when the `/` operator is applied to `length` it can constrain the `Num` typeclass to `fractional`.

```
Prelude> divideLength = 6 / fromIntegral ( length [1, 2, 3] )
Prelude> divideLength
2.0
```

Note: answer is in decimal form as it is of `fractional`

### Type signatures for HOFs

Type signatures are a useful tool to read a function and determines its purpose, it specifies the application of the arguments regarding their respective types.

I found type signature fairly straight forward until I got to the following exercise:

Write the undefined function which will allow this type signature to compile?
```
munge :: (x -> y) -> (y -> (w, z)) -> x -> w
```
At first I got too bogged down with the amount of arrows and letters that were there. it seemed a bit mad.
Then I tried to dissect it logically from the type **signature** (key word).

The output type needs to be of type `w`. So working back from `w`, I need the first element of the tuple `(w, z)` which I can use the function `fst` (a parametric polymorphic function), but that functions require the input `y` and the first argument does just that `x->y` and then `x` is needed to input into the function to get `w`! Therefore if you nest these you get:

```
munge :: (x -> y) -> (y -> (w, z)) -> x -> w -- How to approach this?
munge xy ywz x = fst (ywz (xy (x) ) )
```
Perhaps a bad explanation, but it's hard to explain.
