---
title: "Day 43"
date: 2018-10-15
tags: [Haskell, FP, Guards, HOFs]
draft: false
---
# More Functional Patterns

### Guards
A way of evaluating many truth statements separately. This is an alternative way of using case statements, although this method uses `otherwise` which is ideal for handling *bottoms*.

*Bottoms* - a non-value used to denote that the program cannot return a value or result.

```
avgGrade :: (Fractional a, Ord a) => a -> Char
avgGrade x
    | y>=0.9 ='A'
    | y>=0.8 ='B'
    | y>=0.7 ='C'
    | y >= 0.59 = 'D'
    | otherwise ='F'
        where y = x / 100
```
The pipe `|`syntax here signifies the beginning of a new *guard* case, similar to and `else if` you find in other languages. But different to `if` `then`, `else`, as each *guard* statement requires its own expression for its branch.

### Function composition

This is a neat way of creating *Higher Order Functions* with the composition operator `(.)`.
instead of nesting functions with brackets, the `(.)` operator allows results of functions to be directly into other functions, evaluating left to right.

```
addList :: [Integer]
addList = take 5 . filter odd . enumFrom $ 1
```
The above reads as, enumerate all numbers from 1. Input that as the argument to filter for only odd numbers, then input that into `take 5` which takes the first 5 elements in the list:
```
*Ex7> addList
[1,3,5,7,9]
```

#### Pointfree style

Pointfree is when you don't have data in the higher order functions, but only nested functions. Data isn't inputted until the function is executed.

Although I can't seem to do this with data that is nested in the HOF chain.

For example when trying to convert the above to a pointfree style I can easily take out the `fromEnum` data by inferring it in the type signature:
```
addList :: Integer -> [Integer]
addList = take 5. filter odd . enumFrom  
```
But I cannot remove that `5` using the same method as I get a compile error:
```
addList :: Integer -> Integer -> [Integer]
addList = take . filter odd . enumFrom   
```
The GHC seems to be taking the first argument as the `filter odd . enumFrom` and not the inputted `Integer` from the type signature; as the error message says "Couldn't match type ‘s[Integer]’ with ‘Int’".

**Any ideas how I could make the above into a pointfree style? (without having to add an argument to the `addList` declaration)**
