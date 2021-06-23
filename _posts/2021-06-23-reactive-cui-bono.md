---
layout: post
title:  Reactive - cui bono?
description: Looking back at 8 years of reactive
image: pic01.jpg
---

Recently I experienced the _season_ at the biggest retail company of the Netherlands, bol.com. The season is the period in retail from black friday to christmas where people shop the most. It's when scaling and response times and availability really matter.  
At the same time I've been following Scala and functional programming and the reactive manifesto since 2014. Which promises major benefits in those areas.  

So I thought I'd reflect a bit on _reactive_. It takes a bit of work to be able to program reactively, create reactive systems. So is it worth it? Has it delivered on its promises?  

Reactive _programming_ makes it clear which calls in your system do call other systems and might take a while, might fail. Making sure that your system doesn't tie up resources because of that. And allowing you to be smart about doing those slow calls at the same time. It's about system internals.  
Reactive _systems_ on the other hand change how services interact externally. Not having a long chain of services calling eachother, telling eachother what to do, depending on eachother. But responding to results if and when they become available.  

To do reactive programming well in Scala you need to be well versed in functional programming. And a lot of developers didn't learn that in school. So the benefits need to be worth the organisational effort of hiring developers that know this by heart or getting them up to speed.  
In practice it means that methods return reactive values. And you need to be able to deal with those. Be versatile in `map` and `flatMap` and _monad_'s and how to combine them. For a lot of developers that's an uphill battle.  
So, as an IT manager, it's harder to find developers that are comfortable with all of that.  
Given that it's hard to attract developers as it is, reactive really needs to be clearly worth it.   

I'll just say it out loud: when I joined bol.com nobody cared about reactive programming. We weathered the season with blocking code end-to-end.  

So does that mean reactive programming doesn't matter?  

To a certain degree it does. After all we made it through without major problems.  
All the same I did end up migrating our service to do non-blocking calls. Why was that?  

We needed to make our key endpoint much _faster_. It's an aggregation endpoint that does a lot calls to other services, collecting the state for our application. While implementing user story after user story the calls had been piling up. And when you end up doing 16 calls _after eachother_ it becomes a noticable problem for the customer.  
Reactive programming turned out to be our super power to change the response time of our endpoint from _4.5_ seconds to _0.6_ seconds. Doing most calls at the same time.  
And, importantly, still being able to understand our business logic, the complications of what acceptance criteria. And being in control of how it performs at load in real world conditions.  
Response time was the major pain point that product owners and IT managers cared about. To be honest; being non-blocking did not play a role at all initially.  
Once we had this in place and it performed well under load and under real world conditions like slow dependencies and sudden peaks in RPS it was a good sell to finish what we started. Move all the other calls to be non-blocking as well.  
So what benefit did that bring us? Turns out that to make it through season unscathed we needed a lot of time 1. estimating expected season load, 2. running load test to match, 3. tuning the thread pools of our blocking http clients and circuit breakers.  

Which is the price we paid for a major concern: what if under load we depleted our thread pools? A dependency suddenly becoming ridiculously slow. An unexpected extreme peak in load because of a scarce product becoming available. (The prime example being the Playstation 5. Scarce because of CPU shortage.) Or even worse, the latter causing the former. A perfect storm.   

Making our outgoing calls non-blocking removed all those thread pool tuning concerns. Making us resilient against those scenario's. And sparing us to spend so much time preparing for season.  

So all in all reactive programming turned out to be useful for us. But for product owners and IT managers it's definitely not as much of a must have as the evangelists of the reactive manifesto made it seem.  

_PS_ I'll go into reactive _systems_ in a follow up post.  

_PPS_ With Kotlin coroutines, and Typescript `async` `await`, it's a bit easier. Methods are annotated with the `suspend` keyword.  




