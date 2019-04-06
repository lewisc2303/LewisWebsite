---
title: "Day 54 - Innodays"
date: 2018-10-26
tags: [Innodays, Scala]
draft: false
---
# Innodays 2018!

It has been a while since I last blogged as I was at the HolidayCheck Innodays. Which was so fun, I learnt so much technical stuff and became a lot closer with my work colleagues, t'was was great.

Innodays, was a retreat where a select group of people from all of the HolidayCheck offices met in the Bavarian Alps to work together to produce and most importantly **ship** projects which can benefit the Urlauber.

### Our Project

The project I was involved with was called 'Live Review', which was a service to send push notifications to a mobile device through the browser, with holiday information and review questions. The push notifications were to be sent each day at specific times. For example as the Urlauber is expected to of just checked-in to their room, a push notification would be sent to rate the room and asked whether it was clean. The notification was to be brief and short with the additional option to add further detail, and at the end of the holiday all of these micro-reviews would compile into a full review.

I worked with some very knowledgable engineers that were experienced in tackling a projects like this, albeit a new technology, so research on how to send push notifications was needed.

I was able to shadow the back-end programming which was done in Scala (in a functional manner) and from this I learnt a lot. But in general, observing how the 2 developers approached the tasked and looked up the gaps in their knowledge and debug code was insightful, I hope to be able to incorporate this into my personal learning.

The main technical skills I learnt were:

- How the client-end communicates with the backend using HTTP. I learnt about basic HTTP request methods; `Get`, `Post`. HTTP responses and status codes. However I am going to save further explanation for a later blog post as I think this is a key topic which requires more research and understanding.
- An insight into some Scala web service libraries (Akka - library for web-service and Circe - library for .json files interpretation).
- Using the `future` type to wrap a function in order to allow for multi-threading and prevent blocking. `future` tells the virtual machine to expect a callback value in the future, but in the meantime, to free up the thread for other computation. `future` is usually accompanied by an `onComplete` function which performs a task after the callback has been received. This increases concurrency in the program. This is how asynchronous functions are constructed and are synonymous to 'promises' in JavaScript.

### The Activities

I got up one morning at 6 o' clock to go hiking to the top of the mountain (not Altspitze or Zugspitze but the 3rd biggest I think). It took us about an hour and 15 minutes to the top and we made just in time for sunrise. And it was an amazing site and a great start to the day! See below for a photo of me looking pensive at the top of the mountain.
![Hiking picture](/Images/GarmischPic.JPG)

Every evening we played some board games or role playing games. My favourite of which was "Werewolf". I'm not going to go into how to play the game, but a part is lying. And it was very funny seeing everyone try and lie and convince people of their roles. At first I was terrible at lying but I reckon I got better each night. So you could say Innodays taught me to lie better haha.

### The Food

Now the food... A highlight of the trip. IT WAS INCREDIBLE. Some of the best I've had, and it was mainly traditional Bavarian cuisine, something I didn't know Bavaria had so much of.

I tried:

- Maultaschen
- Käsespätzle
- Kaiserschmarrn
- And loads more...

All sooooo good!

The experience has inspired me to buy a Bayern kochbuch and make some of these dishes myself so I can relive the experience.

The only downside was that I was constantly full and was on an insulin overload, which usually peaked at 4/5pm and made it hard to resist a food induced nap.

### The People

Through working and socialising together I got to know my work colleagues a lot more. A lot of laughter was had :).

#### An all-round incredible experience!
