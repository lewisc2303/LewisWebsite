---
title: "Day 90 - Monoids"
date: 2018-12-02
tags: [Haskell, Monoids]
draft: false
---
# Monoids

This blog post has been in the making for a while as I didn't fully understand *Monoids* to make a Blogpost on them.

### What is a Monoid?

A `Monoid` is a datatype that takes **2 arguments** and is governed by **2 laws**:

- **Applicability** : This law states that the order of argument execution does not effect the result.

```
2+(6+10) == (2+6)+10 == 16
OR ([6,3,7] ++ [4]) ++ [0,8] == [6,3,7] ++ ([4] ++ [0,8]) == [6,3,7,4,0,8]
```
It doesn't matter where the parenthesis are, the results are the same.

- **Identity** : This means that there exists some value called the **Neutral Element**, such that when you pass it as an input to the function, the operation is rendered moot and the other argument is returned *E.g. `0` in the addition of numbers or `[]` in list concatenation*.

**Commutative**: This is when a functions arguments are interchangeable and still yield the same result. **This is not a Monoid law**
Some Monoids are commutative *(Numeric addition and multiplication)*, but they are specific types of Monoids .

The `Monoid` typeclass has 3 expressions:
 ```
class Monoid m where
mempty :: m                       --The identity expression
mappend :: m -> m -> m            --The applicability expression
mconcat :: [m] -> m               --A concatenation expression which utilises the monoidic properties
mconcat = foldr mappend mempty
```

### Semigroups

Semigroups are a superclass of Monoids. And are essentially the same as Monoid but without the identity law, and derives the `<>` method, which is analogous to `mappend`.

```
class Semigroup a where
  (<>) :: a -> a -> a
```

My confusion in this topic was due to the required inheritance of the `Semigroup` superclass in order to instantiate a `Monoid` (something which got implemented in a relatively new version of the GHC). And therefore the `Monoid` typeclass is constrained by the `Semigroup` supergroup.

This confusion also came from me not understanding how to read the typeclass definition:

```
Prelude> :i Monoid
class Semigroup a => Monoid a where
```

Which reads,`a` has the typeclass `Monoid`, **if** it also has an instance for `Semigroup`

An example for an alias of the `Maybe a` datatype :

```
data Optional a =
 Nada
 | Only a
 deriving (Eq, Show)

instance Monoid a => Monoid (Optional a) where
    mempty = Nada

    mappend (Only x) (Only y) = Only $ mappend x y
    mappend (Only x) Nada     = Only x
    mappend Nada     (Only y) = Only y
    mappend Nada     Nada     = Nada

instance Semigroup a => Semigroup (Optional a) where
    Only a <> Only b = Only $ a <> b
```
