---
title: "Day 57 - Strict and Lazy evaluation"
date: 2018-10-31
tags: [Haskell, Lazy, WHNF]
draft: false
---
# Strict, Non-Strict and Lazy Evaluation

#### Haskell can be described as a non-strict language with mostly lazy evaluation.

Aber, Was bedeutet das? (Gestern hatte ich meine erste Deutsche Klasse, also werde ich zufällig Deutsch schrieben, damit ich üben kann)

- **Non-Strict Evaluation**: Non-strict evaluation means that you evaluate an expression from the outside in (as you do in lambda calculus).

- **Strict Evaluation**: Is obviously the opposite, evaluation starts from the inside out.

Therefore in strict evaluation, everything is propagated outwards into the whole expression, therefore if a `bottom` exists in an expression, it will always be found as everything eventually gets evaluated.  

- **Lazy Evaluation**: Evaluating an expression only when its results are needed. So when the expression is created it, the engine makes a `thunk` datatype, which is essentially a dropdown menu for the rest of the expression.

Lazy and non-strict evaluation are nuance, lazy evaluation is non-strict, but non-strict is not necessarily lazy. If a non strictly evaluated expression is created, but all the results need to be evaluated, then it still evaluates from the outside in, but it is not lazy.

**e.g. pattern matching - all results are evaluated upon creation**

Which leads onto...

### Weak Head Normal Form (WHNF)
According to the [HaskelWiki](https://wiki.haskell.org/Weak_head_normal_form), An expression is WHNF when:

- It is a data constructor which will eventually applied to arguments (`Just`, `:`)
- Built in function applied to too few arguments (`(+) 2` or `sqrt `)
- An anonymous lambda expression

Which to me still didn't make much sense when reading it. but when you apply the concept it becomes more clear.

Lists, as mentioned in my previous blog are head-tail recursive about the `(:)` operator and because `(:)` is a data constructer and the lazy evaluation of Haskell, it only gets evaluated up to the data constructer `:`.  However the values contained within them are just `thunk` until the values inside the `:` operator are called, therefore lists exist in the WHNF until the elements in the list are called.

The benefits of this become apparent when applying methods to lists that do not need the values to be evaluated.

e.g.
```
Prelude> length [1, 2, 3 , undefined]
4
```
The above expression still evaluates and does not reach the bottom because the list is in WHNF and the values have not been called.
However if a method that calls the values inside the list was applied, then the list would be evaluated to Normal Form (NF) and throw an error.

```
Prelude> map (+1) [1, 2, 3 undefined]

<interactive>:35:1: error:
```

But this can also be an issue when using `fold`. As folds are evaluated into WHNF before being evaluated to NF, and this can make a very long list and cause stack overflow. But to get around this `foldl'` can be used, which is a non-lazy variant of `foldl`.

#### More on folds in the next post! (I love-hate them)

The non-strictness in Haskell is interesting and hard to get your head around, however inputting a bottom in places can make you understand it better.

E.g. The `(&&)` operator:
```
Prelude> False && undefined
False
Prelude> undefined && False
*** Exception: Prelude.undefined
Prelude> True && undefined
*** Exception: Prelude.undefined
```
As you can see in the above code, the `&&` operator is only non-lazy in its first argument, as it needs to be called to evaluate the expression. And if the first argument enables a result, it will not evaluate the other value and therefore remains as `thunk`.
