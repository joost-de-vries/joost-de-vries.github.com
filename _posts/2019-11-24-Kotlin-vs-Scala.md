---
layout: post
title: Kotlin vs Scala
description: I've worked exclusively in Scala for 5 years. So I was curious to do a Kotlin backend project for more than a year. 
image: pic02.jpg
---

I've worked exclusively in Scala for 5 years. So I was curious to do a Kotlin backend project for more than a year. 

Kotlin does borrow a lot of the improvements to statically typed programming on the Java VM that Scala spearheaded. See Kotlin lead <a href="https://2018.geekout.ee/andrey-breslav/">Andrey Beslavs talk</a> (<a href="https://www.slideshare.net/abreslav/shoulders-of-giants-languages-kotlin-learned-from">slides</a>). Scala was very ahead of its time on the JVM: it started in 2003. Java was then in version in 1.4, did not even have generics. And "Programming in Scala" came out in 2007. While functional programming in Java would only become possible in a bare bones form in 2014 with Java 8. Seven years later.

Less work and workarounds, more enjoyment than Java. That's what Kotlin and Scala share.
For a while I experienced Kotlin as Scala--. Ie as Scala with some features left out. Everything familiar, nothing new when you're used to Scala. Maybe a bit boring.

Now that view has changed. I really enjoy Kotlins extension functions fi. They are possible in Scala, but more cumbersome. Somehow that makes a difference. 

But more importantly; Kotlin has a different approach to reactive programming. When it comes to reactive programming Scala, and Typesafe/Lightbend, have been big proponents of it on the JVM. Creating the Reactive Streams standard f.i. Being in turn inspired by Erik Meijers Rx approach to stream processing. 
So it's not surprising that when the Spring team embraced reactive programming they implemented Erik Meijers stream processing approach for the Spring framework. Conceptually Springs Reactor framework is very much like Rx. And Reactors Mono is very much like Scalas Future. 

Kotlin on the other hand is treading a different path when it comes to reactive programming. Kotlin coroutines make the Kotlin compiler take care of a lot of the reactive programming <code>map</code> <code>flatmap</code> cruft in their coroutines and suspendable functions that a Scala developer would write out themselves.
When it comes to multiple values returned the Kotlin approach is different as well. For communication between threads/coroutines they chose channels. Which are also used by Go and ultimately come from <a href="https://en.wikipedia.org/wiki/Communicating_sequential_processes">CSP</a>. They do employ the equivalent of Rx streams for lazy computations, called <code>Flow</code>s, for the post processing of multiple values. And suspendable functions are the common factor in programming with channels and flows.

I'm very impressed with Kotlins approach to reactive programming. It feels very natural. And it's not a one to one copy of either Go or Rx. Suspendable functions are very much like async/await in say C#, Scala and Typescript. Those don't introduce the notion of a lightweight tread though. 
Scala does have a coroutines implementation from Aleksander Prokopec but that has been abandoned for a few years now. And in the Typelevel world there's a the notion of a Fiber in Scala ZIO.

So why do I think that Kotlin reactive programming is a big deal?
It used to be that the default choice for implementing an application was <em>not</em> to use reactive programming. You'd need a clear goal to choose reactive programming. Because the programming model is harder to grok, you'd need to staff your team with people who are really comfortable with functional programming, with map and flatmap.
With Kotlin coroutines reactive programming can be the default choice. There's no downside. 
Which is probably why Spring made a major push embracing Kotlin, suspendable functions and coroutines in their most recent releases Spring Boot 2.2, Spring Framework 5.2 and Spring R2DBC 1.0. 

Exciting times!

Of course this leaves the topic of reactive systems. Versus reactive programming. But that's a post for another day.

