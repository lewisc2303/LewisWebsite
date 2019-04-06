---
title: "Day 59 - Folds"
date: 2018-11-02
tags: [Haskell, Folds]
draft: false
---

# Folds

Folding is a useful tool for deconstructing data, by reducing about the spine of a list (due to `foldable` being a type-class, folds can also be performed on other datatypes, but this is not in the scope of the fold chapter I just read).

Folds essentially replaces the cons constructor in a list with a function which takes 2 arguments and applies that function through the list until it reaches the base case.

Folds can be represented and understood easier by the following recursive representation:

```
foldr :: (a -> b -> b) -> b -> [a] -> b
foldr f z xs =
  case xs of
    []     -> z
    (x:xs) -> f x (foldr f z xs)
```

As you can see in the above code, the `f` function is applied to the head in the first argument and then the recursive tail, which would eventually end up as a right associated fold when the recursion reaches the base case `[]` , which gets evaluated to `z`.

As blogged about in the last post, folds first evaluates the spine into a WHNF before being evaluated, which can lead to stack overflow if the list is too long. However a strict version of fold exists to prevent this, `foldl'` (`foldr'` also exists but is redundant as the spine needs to be evaluated in order to start reducing the WHNF into NF).

### Scans

Scans can be used in order to show the intermediate stages of evaluation from the fold function.

```
scanl :: (a -> b -> a) -> a -> [b] -> [a]
scanl f q ls =
q : (case ls of
  [] ->[]
  x:xs -> scanl f (f q x) xs)
```

### My issue

In one of the exercises I wanted to recreate the `foldable` method `maximum` which returns the greatest value from a `foldable` datatype (In this case a database list).

```
recentDate' ::[DatabaseItem] -> UTCTime
recentDate' xs = maximum (filterDbGen dbTimeFilter xs)
```
As you can see above, the `maximum` method does this with ease but when recreating it, you cannot use a simple `foldr`. This is because the termination step needs to be the same type as the values in the list, and this is the created datatype `UTCTime`.

```
foldr :: (a -> b -> b) -> b -> [a] -> b
```

Therefore in order to fulfil the type signature, the base case needs to be also `UTCTIme`, so the usual `[]`, `1` or `0` cases do not work.

To rectify this I could either:

- Make the UTCTime datatype inherit the type class `Num` and create an instance of `Ord` for which all of UTCTime is greater than `0` in order to allow for `0` to be inputted as the termination step (A bad work-around).

- Or use a simpler function `foldr1` which doesn't have a base case and hence is a partial function with respect to an empty list as an argument.
But to overcome this, the function could be wrapped in a `Maybe` Type.

And this was the the outcome:
```
recentDate :: [DatabaseItem] -> Maybe UTCTime
recentDate [] = Nothing
recentDate xs = Just (foldr1 f (filterDbGen dbTimeFilter xs))
        where
            f :: UTCTime -> UTCTime -> UTCTime
            f = (\a b -> if (a > b) == True then a else b)
```
