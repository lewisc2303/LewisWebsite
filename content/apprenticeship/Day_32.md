---
title: "Day 32"
date: 2018-10-04
tags: []
draft: false
---

# Data Types

With Haskell being a static typed language and the book I am reading being suitable for beginners, it gives an insight into what types are and why they are necessary.

#### So, why are types important?
Haskell (like Scala) is a static typed language which means any type errors encountered are flagged up at compile time - This makes debugging easier. If the language did not have this, instead it would run into the error at runtime, which is where the code breaks when that function is executed.

Every expression, when evaluated has a type. This type acts as a key to which expressions are compatible with it, so types are a type of abstraction which connect expression compatibilities.

An analogy for types for me is when you play a character on a game, lets say World of Warcraft (which for a period of my life I was addicted to). Certain character types can only learn certain abilities because they are best tailored to that character. If I was a mage, there would be no point learning sword storm, as mages can't wield swords . And if I was a Warrior class theirs no benefit for me to learn pyroblast, warriors can't use magic.

#### Anatomy of a data declaration

```
data Bool = False | True
```

- Type constructor: `Bool`  This is the name of the type and shows up in type signatures.

- Data constructor:`True` and `False`.

#### Typeclasses
Are an an umbrella term for grouping certain types together and specifying which operations can be performed on certain expressions.

By entering `:t (==)` into the REPL, you can find out the type class.
```
(==) :: (Eq a) => a -> a -> Bool  
```

The typeclass here is `Eq` . And the above definition reads as:
If the type 'a' is of `Eq` class then `(==)`will take any 2 variables and returns a `Boolean`  
