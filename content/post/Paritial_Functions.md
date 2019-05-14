+++
title =  "Partial Functions"
date = 2019-05-13T18:00:19+02:00
tags = []
featured_image = ""
description = ""
+++

# Partial Functions

So I have started a Udemy course on called [Rock the JVM! Advanced Scala and Functional Programming](https://www.udemy.com/advanced-scala/learn)

In this course it teaches advanced functional methodologies in Scala.

The first topic is **Partial Functions**

*"A partial function is a function that does not provide an answer for every possible input value it can be given. It provides an answer only for a subset of possible data, and defines the data it can handle."* - [Alvin Alexander](https://alvinalexander.com/scala/how-to-define-use-partial-functions-in-scala-syntax-examples)

Basically, a partial function is one that the function does not map a co-domain to all existing domains. So only has solutions to some of the input.

Scala defines it as:

*A partial function of type PartialFunction[A, B] is a unary function where the domain does not necessarily include all values of type A. The function isDefinedAt allows [you] to test dynamically if a value is in the domain of the function.*


The trait type declaration:
`trait PartialFunction[A, B] extends (A => B)` 

Therefore the intended domains can be directly mapped to scala cases as it type matches the first order function type definition `A => B`.

This can be seen here:

```
val partialChatFunctionType: PartialFunction[String, String] = {
    case "HI" => "Oh hi there"
    case "HOWDY" => "why howdy ya'll"
    case "WASUP" => "Sup my man"
    case "SERVUS" => "Hallo, wie gehts?"
  }
```

Scala wraps this functional concept in a type which allows you to safely handle the *bottom* case (non-mapped domains) with methods such as `Lift` which when used on the partial function calls, returns an `Option`. Or `applyOrElse` which when a non-mapped domain is inputted, a default domain in used as a fallback.

```
stdin.getLines()
    .foreach{
      lines => println(partialChatFunctionType.lift(lines))
    }
```

Partial functions can be chained using the `orElse` to deal with other domain cases for the same input like an `||` statement. 

```
val isEven: PartialFunction[Int, String] = {
     case x if x % 2 == 0 => x+" is even"
}

val isOdd: PartialFunction[Int, String] = {
     case x if x % 2 == 1 => x+" is odd"
}
val numbers = (1 to 10) map (isEven orElse isOdd)
```

Below is the same as creating the type safe pattern match yourself:

```
val partialChatFunction = (input: String) =>
    input match {
      case "HI" => Some("Oh hi there")
      case "HOWDY" => Some("why howdy ya'll")
      case "WASUP" => Some("Sup my man")
      case "SERVUS" => Some("Hallo, wie gehts?")
      case _ => None
    }
```

**But** without the reusablility of the abstracted type or the typeclass methods that come with it.