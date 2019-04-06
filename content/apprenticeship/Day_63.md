---
title: "Day 63 - Algebraic Datatypes"
date: 2018-11-06
tags: [Haskell, Datatypes]
draft: false
---

# Algebraic Datatypes

The strict type system of Haskell is one its key features, it can aid in crafting HOFs, catching errors at compile time and allow for more descriptive code.

Algebraic Dataypes can be categorised into 2 main types:

#### Sum Type
A data structure that contains different fixed singular data constructors. The most familiar being Boolean.

```
data Boolean = True | False
```

*When no arguments are required for the type constructor, it is referred to as a nullary constructor*

As you can see the notation used is the `|`, which essentially means "Or".

#### Product Type
A datatype which is composed of two arguments, which are both required to satisfy the data constructor. Examples of these are Tuples or Records

```
data Product = Record a b

--or

data Product = Tuple (a, b)
```

*Unary constructor is a term used, when a type only takes one argument*

#### Cardinality

The possible outcomes of a function based on data constructers. If it is a `product` type, then the cardinality is the product and in `sum` type, the sum, hence the naming.

The reduction in cardinality can help with reducing the possibility of edge cases, as the number of possibilities is controlled.

#### Type Aliases

Type Aliases are used to make the code more descriptive, and basically allows for alternate naming of types.

```
type String = [Char]
```

### Kinds

Kinds are confusing to me and I don't fully understand them. But my interpretation is that they are a level higher than types. The kind of a type is basically the type signature but even more vague. A `*`  represents a space for a concrete value and so a kind signature can only have 2 kind constructors `*`and `->`.

You can use `:kind` to query a type constructor. Similar to how you can use `:type` to query a data constructor.
```
Prelude> :k Bool
Bool :: *
Prelude> :k []
[] :: * -> *
```

### Language Pragma

Are extensions to the Haskell GHC to allow for variations to the compiler. These of course, should be used with caution.

The ones I used was the `{-# LANGUAGE FlexibleInstances #-}` which allowed me to write instances of a type, that I couldn't before.


### Binary tree

Binary tree is essentially a Type variation of the lists.
The Binary tree is a `Sum` type of a base case data constructor and a recursive constructor, analogous to `data [] = [] | : [a]`.

The advantage of a binary tree is that it can be constructed in both the `left` and `right` direction.

Below is an example of the `map` function using a binary tree.

```
data BinaryTree a =
    Leaf
    | Node (BinaryTree a) a (BinaryTree a)
    deriving (Eq, Ord, Show)

mapTree :: (a -> b) -> BinaryTree a -> BinaryTree b
mapTree _ Leaf = Leaf
mapTree f (Node left a right) =
    Node (mapTree f left) (f a) (mapTree f right)
```

I have yet to understand a situation where I would need a binary tree over a list. In my opinion, it adds an additional unneeded layer of complexity.
