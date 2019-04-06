---
title: "Day 24"
date: 2018-09-26
tags: []
draft: false
---
# Day 24
```

val headacheMap = Map("FunctionalProgramming" -> 5 , "Scala" -> 2, "DealingWithKVR" -> 5)
val headacheScore  = headacheMap.foldLeft(0)(_+_._2)

def headacheStatus (headacheScore: Int): String = {
  if (headacheScore > 10) "I've got such a headache"
  else if (headacheScore > 5) "Managable"
  else "Chilling"
  }
headacheStatus(headacheScore)

```
