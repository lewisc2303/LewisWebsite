---
title: "Day 44"
date: 2018-10-16
tags: [Haskell, FP, Recursion]
draft: false
---

# Recursion

Is the use of repeated function application, so the self-calling nature of a function. Recursive functions requires a a termination step to avoid stack overflow. The usual layout of this is to make a recursive bottom and the termination steps higher up the code order.

Today I saw myself naturally implementing a TDD approach (very loosely because I'm not even implementing test suites into Haskell rn) to creating my recursion model.

The exercise was to write code which converted a number of any size into its a string with each individual digit spelled out.

The recursive section was the `Digits` function.
And at first I wrote it in steps, compiled it and ran manual tests.
Starting with converting a number with a size of 1 digit, then 2, then 3, until I started seeing a pattern emerge, and then I refactored with the recursion.

```
digits :: Int -> [Int]
digits n = [dig3, dig2, dig1]
 where
    dig1 = snd (divMod n 10)
    dig2 = snd (divMod (fst (divMod n 10)) 10)
    dig3 = snd (divMod (fst (divMod (fst (divMod n 10)) 10)) 10)
```

Which when fully refactored became:

```
digits :: Int -> [Int]
digits n
 | (fst (dM) == 0) = [ snd (dM) ]
 | otherwise = (++) [(snd (dM))] (digits (fst (dM)))
    where
        dM = divMod n 10
```

What I liked about this exercise is that it combined both recursion and HOFs :)

```
module WordNumber where

    import Data.List (intersperse)

    digitToWord :: Int -> String
    digitToWord n =
        case n of
        0 -> "zero"
        1 -> "one"
        2 -> "two"
        3 -> "three"
        4 -> "four"
        5 -> "five"
        6 -> "six"
        7 -> "seven"
        8 -> "eight"
        9 -> "nine"       

    digits :: Int -> [Int]
    digits n
     | (fst (dM) == 0) = [ snd (dM) ]
     | otherwise = (++) [(snd (dM))] (digits (fst (dM)))
        where
            dM = divMod n 10



    wordNumber :: Int -> String
    wordNumber = concat . (intersperse " - ") . (map digitToWord) . reverse. digits
```
