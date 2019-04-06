---
title: "Day 95 - Data Ingenieurwesen && Meine Haskell Umwelt"
date: 2018-12-07
tags: [Haskell, DataEngineering]
draft: false
---

# Data Engineering

So this week I joined the Data Engineering team. Their main role is to maintain and refine data for both internal and external purposes.
There seems to be quite a bit of complex technologies and frameworks which are intrinsic to the data team such as the data import scheduler and Spark.

I had heard of Spark before and but only that it was used in big data distributed data computation, but never seen it, or looked into how it works.
One of the Data Engineers showed me Spark and the spark shell, which seems cool, although, I really want to watch some videos about Data Engineering and read some stuff in my spare time so I can make the most of this opportunity but just haven't found the time. But I'm planning to dig into it at the weekend and hopefully understand the tools a bit more. Maybe look into how distributed processing works, as it seems very functional from the terminology I've heard such as `mapReduce`: Where a big data computation is split into lots of map function and then reducing the outcomes of the map distributed processes to a result. I guess Big Data has to be done in a functional way to optimise processing time.

**again I'm rambling**

# New Haskell Environment

Something that I missed from when I was using python, were IDE extensions which allow for linting, autosuggestion and and styling. I guess it's been good not having this at the beginning as it has allowed me to understand the compiler better and how to deal with the complier error messages.

I first tried to download "Haskforce" on IntelliJ, but realised that a GHC extension "GHC-mod" and "GHC boot" had not been updated for the newest GHC version.
I then tried some of the VS code plugins, both "Haskell Language Server" and "Haskelly" and I ran into similar issues.

But eventually I got Haskell Language Server to work. And the issues above were overcome by using the hie-wrapper rather than the hie itself. Which to my understanding is a plugin that runs in the background, but has to be manually added to the bash $PATH and then in the VS-code settings linked to this path.

https://github.com/alanz/vscode-hie-server/issues/105

WELL! This took me a lot longer then I intended. but it is done now and I'm happy with the result, coding in Haskell is going to be much easier with type signature hover display, method auto-suggestion and auto-formatting! It even highlights an equation if it can be made pointfree.

But through doing this I learnt a lot about the Haskell project and package management system whilst troubleshooting.
Predominantly, the difference between Stack, cabal and resolver. And how the Haskell version snapshot system works, which I shall summarise below:

**Cabal** usually refers to the Haskell package manager and it allows for libraries and packages to be stored and imported into Haskell projects. But it can also refer to cabal-the-spec *(.cabal files)*, cabal-the-library *(code that understands .cabal files)*.

### But more importantly, Stack and Stackage:

**Stack** is the build tool for Haskell which allows you to build a project via the information in the `Stack.yaml` and `package.yaml` file, which is configured so that it references a certain snapshot of the Stackage package library. This snapshot is determined by the `resolver` field in the `stack.yaml` and would usually be something like:
`resolver: lts-12.21`
The `lts` prefix means "Long Term Stackage" which means that the particular Stackage snapshot has been tested with all the package versions contained in that snapshot. This allows for reassurance that a particular project will always work, even in the future when packages create new revisions.

However there are often cases where you need packages or other versions that are not included in that particular snapshot/resolver and therefore need to add it explicitly in `extra-deps` like:

```
extra-deps:
- conduit-1.2.13.1
- conduit-extra-1.1.17
- resourcet-1.1.11
- streaming-commons-0.1.19
```
Usually the complier will prompt you when you need to add package versions to the `extra-deps` section but if not you can check which packages are supported by a particular Stackage snapshot [here](https://www.stackage.org/).
