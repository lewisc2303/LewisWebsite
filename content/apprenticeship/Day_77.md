---
title: "Day 77 - MuniHac 2018"
date: 2018-11-19
tags: [Haskell, Hackathon]
draft: false
---
# MuniHac 2018

Once again I've been lacking on my blog posts, but since I am on a 3 hour coach journey, it is a great opportunity to write about my MuniHac experience.

#### MuniHac is a 3 day Haskell Hackathon:
**One room, 80 Haskellers, unlimited food and coffee and a passion for immutable datatypes.**

# Day 1

With this being my first hackathon, I felt a bit nervous as I didn't know anyone there and was not sure on the levels of Haskell competency.
But when I first arrived and got chatting to people, my nerves were set at ease. Everyone was very chatty and were welcoming to all levels and the level of Haskell was varied; from beginners still at university to experts contributing to the GHC (Glasgow Haskell Compiler).

The event started with participants presenting projects they were working on, which ranged from exploring libraries, creating libraries, breakable toys, to fixing GHC bugs. There were also beginner workshops on the first day, which were geared towards those whom have little/no Haskell experience. Which after attending the first workshop, realised it was indeed *beginner* and I may be more on the upper beginner/intermediate boundary, and so I went out into the main room to join a project group.

### Idris

During the project bidding, I remembered this group which were going to explore the *Liquid Haskell* library and *Idris*. I didn't know what Idris was but I'd heard of *Liquid Haskell*. A library for creating refined types through predicates, the only predicates I knew how to use is from [list comprehension](https://lewis-coleman-blog.netlify.com/post/day_56/), but liquid Haskell uses predicates to limit enumerable values from being accepted on a type level *which is pretty cool and useful*.

Although we didn't touch Liquid Haskell, I spoke about it with people and will definitely be something I shall look into in the next few weeks.

Instead we played around with a Language called Idris. Idris is a functional language with very similar syntax to Haskell but with *dependant types* which has some Mathematical nuances when compared to Haskell which I don't understand. **But** my take-away was that it allowed for concrete values to be incorporated at type-level (making it easy to create refined types) but also allowed the compiler to predict pattern matching based on the type signature, through proofing, using the `?` syntax. This made for a cool pattern matching exercise where you can pattern match complex functions by interpreting the compiler type checker. Further information can be found here >> docs.idris-lang.org/en/latest/proofs/patterns.html .

**^^Possible idea for a pattern matching game for all the apprentices to participate in**

In the evening there was of course dinner and a few drinks.

# Day 2

On the second day I went back to Haskell. And carried on with my 'To-Do task' but on the same table as the Idrisers and some other Haskell projects, one of which was creating a library for specific generics *(will explain later on in the blog)*. This way I got to see what other people were doing on these more difficult projects and join in table on conversation whilst doing my own project.

Whilst creating my project I had to dive into... **MONADS**. Something that when I asked a few different people to explain, I got a pause followed by *"Well" "They are like `functors` and `applicatives`", "They are data containers" "They encapsulate side effects", "They can preserve state"* . Most of which, out of context, didn't fully make sense. But what it did make me understand, is that most of them don't KNOW the theory behind Monads, but knew how to use them and their purpose. And that's what I had been doing with `IO a`.

### IO

![Monad meme](/Images/MonadMeme.jpeg)

`IO a` monad encapsulates side effects allowing you to know which is a pure and impure function. It is like a wrap on the type level but actually doesn't effect anything on the data constructor level.

But something I did learn is chasing the `IO`, once an `IO` is introduced, it protrudes through your type signatures like a spot you cant get rid of. until you eventually push it out back into the impure world by externalising the result. Ideally you want to keep your functions as pure as possible, which can be done by separating your impure and pure functions.

### Generic datatypes

During the 2nd day there was a 2 hour talk on generic datatypes. Something that, I had read about and keep hearing in conversation but just got stored into my personal backlog of *"Concepts I don't understand, but not gonna worry about now, maybe look up later"* (It's currently a big backlog).

**The Hackage definition is:**

*Datatype-generic functions are based on the idea of converting values of a datatype T into corresponding values of a (nearly) isomorphic type Rep T.*

My understanding of it is that it moves functions declarations into the type level so that you can create instances of a isomorphic method for different types rather than just for concrete functions.

for simple cases most of the hard work is done for you by `deriving` the `Generics` type-class. But of course there are so many cases where its not simple `-_-` .

An application of the above, is data serialisation and deserialisation.

# Day 3

This day was the wrap up day where people presented what they did during the Hackathon, and a lot of it was interesting, albeit 80% went over my head.

But as I started to finalise my To-Do project, I realised I need to data serialise my to-do list into a `.txt` file and de-serialise it back. When asking around it seemed that no one has really done that and they tend to just serialise to `.JSON` instead of `.txt` using the [Aeson](http://hackage.haskell.org/package/aeson) which uses generics and state monads `:o`. But apparently it isn't bad at all to use, because all the scary stuff is done behind the scenes.

Although I am stubborn and also want to look for a library to `.txt` (de/)serialise. One does exist but is less used [Text.Parse](http://hackage.haskell.org/package/polyparse-1.12.1/docs/Text-Parse.html).

![MuniHac2](/Images/MuniHac2.jpeg)
This is us struggling with the `stack.yaml`. The pensive look is not deliberate, I swear.

#### Some items added to my personal backlog from MuniHac:
- Linear types
- Liquid Haskell
- Recursion schemes
- Look into the Acme library (loads of stupid stuff like errors that are frowny faces)
- Applicatives
- functors
- MONADS
- Servant library (A library for type level APIs)

## Summary

Great first hackathon, learnt a lot, met and spoke to a lot of people about how they use Haskell, why they love Haskell and how they learnt it. All of which has given me fuel to carry on and continue to develop my Haskell knowledge.

DISCLOSURE: A lot of this is an oversimplification, maybe to the point of making false claims. So don't take this as gospel.
