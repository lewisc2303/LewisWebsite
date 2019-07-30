---
title:  "Evaluation Strategies"
date: 2019-07-29T17:57:10+02:00
tags: [ Scala, FunctionalProgramming, Lazy ]
featured_image: ""
description: "To use Scala in a functional way, knowing how to optimise code evaluation is important and something I do not currently do. So this is me trying to understand and use it correctly."
---

# Evaluation Strategies

### Introduction

Inspiration for this topic came from a few Scala courses I have taken and previously brushing over and accepting the different "call-by" evaluations without digging into them.

So in this blog post I shall dig into the generic categories of evaluation stratgies and then go into the individual types and write some example code to annotate the concepts.

### Strict or Non-strict evaluation

The difference between the 2 in a nutshell:

- *strict* evaluates from the inside out, and therefore everything gets evaluated.
- *non-strict* evaluates outside in, so if the desired value is reached before evaluating the whole expression, not everything is evaluated.

[I have wrote about this topic before during the apprenticeship whilst I was learning Haskell.](https://www.lcoleman.me/apprenticeship/day_57/)

### Call by Value (Strict)

This is the default evaluation for JVM languages and hence the default in Scala.
In this type of evaluation, when a value is assigned it is saved in stack memory and fully evaluated at the point of assignment. So when this value is then executed again, it just returns the value and does not re-evaluate.

### Call by Name (Non-strict)
In this case the value is called upon by the use of the argument and not upon assignment. So when this argument is needed as an argument, it is evaluated and then every time the value is called again, it is re-evaluated.

This can be demonstrated by seeing whether an error gets evaluated:

```
trait EvaluationStrategiesForError{

  def error(): Unit = {
    throw new Exception
  }
  def callByValue(arg: Any): Unit = {
    println("output")
  }

  def callByName(arg: => Any): Unit = {
    println("output")
  }
}

object evaluationErrors extends App with EvaluationStrategiesForError {
  println("callByName: ")
  callByName(error())

  println("\ncallByValue: ")
  callByValue(error())

}
```

This outputs:
```
callByName: 
output

callByValue: 
Exception in thread "main" java.lang.Exception
```

So as the error was never used in the function, it was never evaluated.

*Within the JVM, some weird stuff happens to make this so, I looked into it but my ability to understand Java bytecode, is and for now will remain non-existent*

### Call by Need (Non-strict)
This is the default evaluation for Haskell. But can also be created in Scala by using call by name arguments with lazy vals.

This implementation has the benefit of lazy evaluation through 'call by name' but caches the argument for re-use.

The example below best shows the benefit:

```
trait EvaluationStrategies {
  def something(): Int = {
    println("calling...")
    42
  }
  def callByValue(arg: Any): Unit = {
    println(arg)
    println(arg)
  }
  def callByName(arg: => Any): Unit = {
    println(arg)
    println(arg)
  }
  def callByNeed(arg: => Any): Unit = {
    lazy val byNeedValue = arg
    println(byNeedValue)
    println(byNeedValue)
  }
}

object evaluationCache extends App with EvaluationStrategies {
  println("callByValue: ")
  callByValue(something())

  println("\ncallByName: ")
  callByName(something())

  println("\ncallByNeed: ")
  callByNeed(something())
}
```

Running this script outputs:
```
callByValue: 
calling...
42
42

callByName: 
calling...
42
calling...
42

callByNeed: 
calling...
42
42
```

### JVM evaluation and storage

JVM deals with primitives and objects in different ways:

- **Primitives** (*String*, *Int*): Are stored inside the stack memory (the memory space that holds method-specific variables that are short-lived in addition to references to other objects in the heap).

- **Objects** (*instanciated classes*): The object data is stored inside the heap memory (the memory space that holds objects and JRE classes), and a reference for the object is kept inside stack memory, which just points to the actual object.

### Call by Reference

Although this does not exist in the JVM, for that sake of covering the whole topic, call by reference is where the memory address of the variable is passed into the function call as the actual parameter.

The JVM  does manipulate objects by reference, and all object variables are references. However, Java doesn't pass method arguments by reference; it passes them by value.


---

*These concepts become more interesting when applying them by strict and non-strict data structures, but will save this for another blog post.*

#### References: 

- https://rockthejvm.com
- https://dzone.com/articles/java-pass-by-reference-or-pass-by-value 
- https://www.javaworld.com/article/2077424/learn-java-does-java-pass-by-reference-or-pass-by-value.html