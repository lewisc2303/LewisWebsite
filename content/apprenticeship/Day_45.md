---
title: "Day 45 - Exercism"
date: 2018-10-17
tags: [Haskell, FP, Recursion]
draft: false
---
# A break from the book

Today I've been completing some more autonomous and less guided exercises in [Exercism](https://exercism.io/my/tracks). I find these exercises more challenging as it's not focused around the last chapter I read, and forces me to apply everything that I've learnt and work out the best way.

An example is the Acronym challenge, which requires you to create a function that creates an acronym out of any `String` argument.

The exorcism download has pre-built tests which really test all the edge cases, and made me develop the code further.

The 2 tests that made me have to develop my code were:

- HyperText Markup Language -> **HTML**
- Complementary metal-oxide semiconductor -> **CMOS**

Although I managed to satisfy all tests, my code doesn't look as clean as it could be. I had to do some work-arounds to satisfy the `++` type restriction of `[a] -> [a] -> [a]` by making the the `head` of `word` `[char]` by making it a one character list.

```
import Data.Char

abbreviate :: String -> String
abbreviate word = go word [] ' '
    where go word acronym lstChar
            | length word == 0 = ""
            | (isUpper lstChar) && (isUpper currentChar) == True = go restOfWord acronym currentChar
            | ((lstChar == ' ') || (lstChar == '-')) == True = acronym ++ ([toUpper currentChar]) ++ (go restOfWord acronym currentChar)            
            | isUpper currentChar == True = acronym ++ ([head word]) ++ (go restOfWord acronym currentChar)
            | otherwise = go restOfWord acronym currentChar
                where currentChar = head word
                      restOfWord = tail word
```

Next post shall hopefully be about referential transparency. Because recursion to me seems to break this fundamental, so I am going to research into this and write a blog post about it tomorrow.
