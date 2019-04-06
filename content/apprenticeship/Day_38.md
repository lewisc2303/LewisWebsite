---
title: "Day 38"
date: 2018-10-10
tags: []
draft: false
---

# Typeclasses

This chapter (eventually) made me understand the Haskell type system a lot more.

#### Main Typeclasses:

- `Eq` = For determining equality of values. Applies to most (maybe all) prelude datatypes. Methods: `==` or `/=`
- `Ord` = For comparing values. A sub class of Eq as equality determination is needed to compare. Methods: `> < compare min max`
- `Num` = For basic arithmetic. Superclass for most numeric types. Methods: `(+) (-)`
- `Enum` = types that have predecessors and successor elements. Methods: `FromEnum`, `enumFromThenTo`
- `Show` = typeclass which allows types to be printed to the terminal. Creates `Show a => a -> String` (prints type as string)

I previously thought of types and typeclasses as a kind of stem and branch model, but rather it's an inheritance models where types derive methods from parent classes but can derive many different parent classes rather than just from the one stem.

### Instances

If a type is said to have an instance of a typeclass, it means that it has access to its methods.

The data type must first be declared with the syntax `data` and then the data constructors are stated.
And then the `deriving` clause is used to generate standard instance declaration of that typeclass to the datatype.
```
data Colour = Red | Blue | Green deriving Show
```
**Colour:** Type Constructor (analogous to Bool)

**Red | Blue | Green:** Data constructors (analogous to True | False)

However specific instances can be pulled from a typeclass by using the `instance` declaration.

```
instance Eq Colour where
  (==) Green Green = True
  (==) Blue Blue = True
  (/=) Red Red = True
  (/=) Red _ = False
  (==) _ _ = False
```
*(I've made the logic weird just to demonstrate that the methods inherited can be crafted different to the derived instances)*

The problem with the above is the possibility of making partial functions, which are functions which can't evaluate for all possible cases. To try and catch these, the `:set - Wall` command in the prelude can be performed to let the GHCI identity partial functions.

*I struggled at first with this chapter because I think I was trying to go too fast. When I went back and made the connection to what I knew and compared everything to the standard; type constructor, data constructor format I learnt from the previous chapter, it clicked*

**Something that still confuses me is how `IO()` works, I get that it is for managing side effects and used when printing to the console, but HOW does that manage side effects? Any answers, please post in comments ;)**
