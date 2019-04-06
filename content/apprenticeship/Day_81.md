---
title: "Day 81 - RSS :(, Haskell :)"
date: 2018-11-23
tags: [Haskell, RSS]
draft: false
---

# RSS failed :(

So yesterday I made an RSS feed for my blog, but for some reason it does not work. I think the theme I am using is not explicitly made for RSS as some of the other apprentices struggled with this theme too. Therefore I have started setting up my new theme and will hopefully finish it on Monday.

# Looking into a Haskell Service

Today a fellow HolidayCheck employee showed me a HolidayCheck service which was created in Haskell which was cool to see. It used a lot of the libraries I had heard about from MuniHac. Predominately; Servant, Aeson and Http-client.

Something I realised when going through the code and looking at mine, is that I am not testing properly. Part of the reason is that I am not writing in a TDD style. I started off doing it, but I guess I got disctracted with implement new bits of code, that I stopped writing tests. Back to TDD :).

It was also good to see `Maybe` and `Either` used in the correct way to error handle. In my ToDo task I saw the `Maybe` type as a nuance. Which made me think that even though I've done all this Haskell theory, I haven't actually practiced it enough, or viewed other Haskell code, to comfortably write in a true Haskell manner.

So I dedicated a lot of the day to doing Kata (whilst writing tests!) and searching GitHub for Haskell code.

### Etwas Deutsch

Heute bin ich aus England arbeiten, weil ich ein neue Nichte. Deshalb, diese wochenende werde ich ihr sehen.
Sie ist sehr süß! 
