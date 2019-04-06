---
title: "Day 65 - My Haskell Genesis"
date: 2018-11-08
tags: [Haskell, IO, do]
draft: false
---
# Today I made my first Haskell Project !

It was a text-based hangman game, and it was heavily guided by the book, even-so it brought everything together and it was quite cool actually producing something tangible.

So the basics for setting up any project is by the following commands:
```
stack new my-project
cd my-project
stack setup
stack build
stack exec my-project-exe
```

- `stack new` builds a project directory for a new Haskell Project
- `stack setup` will download or update the necessary GHC compiler
- `stack build` will build the minimal project in order to execute teh project.
- Then depending on what executable command you give the project in the .cabal file, `stack exec` will execute your project.

#### The .cabal file
This file is a file in the project directory to document build and library dependencies and write executables. By using the stack build commands above, a pre-configured .config file is created.

### Basic terms to know pre-monad enlightenment

#### IO
As touched upon in previous blogs, the `IO`  (Input/Output) type is used to control side effects and keep them explicitly separate to other types.
methods that inherit the `IO` typeclass are usually defined as a Unary constructer with a Type signature of `IO a` which when used with a binding `<-` becomes type `a` (binding is a way of equally the output of a `IO a` method to a value of type `a` (this is very simplified, as I do not yet understand Monads).

#### do

`do` is syntactic sugar to sequentially order function calls. They make things more readable by explicitly showing in what order things are being called.

The `main` function is the one that usually needs to introduce side effects, by either pulling data or reading from the console. Therefore it is usually the case that this would be a `do` block of type `IO`

```
main :: IO ()
main = do
  name <- getLine
  return name
```

#### Key bits

To make import aliases: `import qualified Data.Bool as B`

`return`, returns a `monad` value in IO. Without it, the value would not be returned.

`forever`, from the Control.Monad library allows the creation of an infinite loop, analogous to a While loop.

`exitSuccess` from the System.Exit library is a safe way to exit the programme.
