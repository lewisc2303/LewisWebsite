---
title: "Day 73 - Testing"
date: 2018-11-14
tags: [Haskell, Testing]
draft: false
---

# Testing in Haskell

As in any language, testing is crucial for driving and creating good, maintainable code. And for me, this would be the only criticism of the book, the testing chapter, for being both too vague with the specific implementation with regards to test layout and for introducing it so far into the book.

Throughout the book, functions were tested by loading the file into the GHCi and interpreting the compiler error, which is essential to a strictly typed language. But it hasn't allowed me to code in a TDD manner.

Saying that, I LOVE the book and it's taught me a lot of core principles that were lacking in my knowledge base

### HSpec

The testing library I have been using is [Hspec](https://github.com/hspec), for no particular reason, it's just the one the book recommended. However their is [Tasty](https://github.com/feuerbach/tasty) which I've come across which I might explore at a later date.

Hspec supports both property (property testing is idiomatic to Haskell and strictly-typed languages) and unit testing.

### My issues

I ran into many issues when implementing `hpec`, below are the 3 root causes :

#### package.yaml Vs .cabal

As far as I am aware, the `package.yaml` and `.cabal` files are both build files and serve the same purpose, but editing both of them can interfere.
The actual definition can be found [here](https://docs.haskellstack.org/en/stable/stack_yaml_vs_cabal_package_file/) which states `package.yaml` file is a bit more abstracted version of the `.cabal` file and therefore the `.yaml` file should be used.

**Issue 1**

I was adding dependencies to the `.cabal` file and it was throwing a warning error message.

#### Project Layout

In Haskell the layout of a project should be done in a way where you have all your functions in the library and only a very small `main` executable in the `app` directory, which executes functions by importing the library.

**Issue 2**

I had the main bulk of my code in the main directory and, you cannot import the `main` directory into your testing spec.
And my spec file was called `LibSpec.hs`.

#### Test Layout

When writing tests with hspec, on execution it automatically looks for a `main` function in a file called `Spec`.

However a better way to implement Hspec and enable a clear test structure which reflects the `src` directory is to use *Automatic spec discovery*
This is where a file called `Spec.hs` is inserted in to the `test` directory with the test executable in the `package.yaml` directed towards this file, and a Language Pragma written inside:
```
{-# OPTIONS_GHC -F -pgmF hspec-discover #-}
```

This Language Pragma basically searches all of the files inside the `test` directory ending in `spec` for functions with the function name and type signature `spec`:

```
spec :: spec
spec = undefined
```

This way, whenever you execute the tests `stack test`, all of the tests are executed at once.
A good practice for test layout is to create a test for each source code you have.

E.g. `LibSpec.hs` , `TypeSpec.hs` to correspond to the source code files `Lib.hs` and `Type.hs`

**Issue 3**

Not doing the above!
