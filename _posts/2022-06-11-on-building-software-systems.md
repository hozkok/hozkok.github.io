---
layout: post
title:  "On Building Software Systems [Draft]"
date:   2022-06-11
---

In this post, I discuss the problems and considerations to take in designing and building systems.

## The problems of software systems

One of the biggest problems in building software systems is that people not necessarily think as much in detail about the evolution of the systems they build as they are supposed to. This might have several reasons such as, tight deadlines, poor architecture, lack of experience to have confidence enough to say "no", lack of theoretical knowledge and/or simply not having a "good taste".

Having poor decisions and practices eventually cause the entire systems to fail. Software systems will evolve. In a good or bad direction. And it is in our hands to decide their fate.


## The Architecture

The biggest effort we should probably start with is the simplicity of the software and systems' architecture. Simplicity is hard. And needs time and careful consideration.

> Simplicity is the ultimate sophistication. <br/>*- Leonardo Da Vinci*

### Software Architecture

It can be vitally important on how we structure and evolve the architecture of the software we build. How do we define modules, object ownerships, dependencies, tests. How open our structure to extension?

Coming up with decisions involve the thought process on how we approach to the programming. Languages shape our thought procecss. The entire paradigm space we have. The good practices differ in languages and frameworks. It is **very** important that how do we structure and evolve the architecture of the code base.

Some popular backend frameworks (such as django, rails, phoenix, laravel) have very opinionated approaches on the structure. This helps people to jump into the projects quickly if they know about the framework. The frameworks make many decisions for you on where to define constructs. But as the code and the requirements evolve, coming up with more specialized architecture will be inevitable. Will be harder to fight the complexity, there will be constraint on time, and sometimes it won't be obvious to see the patterns and see the simple abstractions and correlations. Moreover, if you follow services architecture, more and more specialized structures will be needed depending on the scope and purpose of the system.

#### Structure as Directed Acyclic Graph (DAG)

<figure>
    <img src="/images/directed-acyclic-graph.png">
    <figcaption><a href="https://en.wikipedia.org/wiki/Directed_acyclic_graph">[image from wikipedia]</a></figcaption>
</figure>

In the modern world software systems, most of the applications have complex data-driven logic. And when it comes to data, having cyclic relationships is extremely harmful and hard to manage. DAGs are very popular data structures for data pipelines and immutable structures. If two data models depend on each other, there is probably an association that needs to be defined separately. If you have a cyclic relationship, you probably have a bad smell ([taste](#having-a-good-taste)) in the architecture.

### System Architecture

When we build a system [of systems], how we define dependencies play a very important role on the complexity and reliability of the system. **Minimizing the moving parts** is one of the most important things and we should be conservative when it comes to introducing a new system level dependency for the new requirements. A new system level dependency potantially means more metrics, less fault tolerancy, less control over the system.

As with most things, simplicity is important. When it comes to systems architecture, simplicity is even more important. And a software system's simplicity starts with its system architecture. Once the system evolves into a complex system, there is no turning back. Fighting the complexity while evolving for the current needs is usually **infeasible** as discussed in the famous [Clean Code by Robert C. Martin](https://www.goodreads.com/book/show/3735293-clean-code).

As stated by the famous Gall's Law;

> A complex system that works is invariably found to have evolved from a simple system that worked. A complex system designed from scratch never works and cannot be patched up to make it work. You have to start over with a working simple system.
> <br/> *- John Gall*

## Choosing the Programming Language

This is probably less important than the architecture, but still is an important decision to make. Historically, the fight on programming languages is as old as the programming itself. OOP, FP, imperative, declarative, structural programming... Fight goes on.

From the engineering perspective, There is a trade-off between "safety" and "productivity". Languages evolve in a way to find the middle ground in this trade off. Modern languages like Rust, C#, (new JVM languages like Scala, Kotlin) try to find the sweet spot, while in the far end of the safety spectrum Haskell carries the flag. Some languages come from academia, some from [hacker culture](https://en.wikipedia.org/wiki/Hacker_culture). And historically, most of the useful languages that are still widely adopted and still alive come from the latter.

So how do we consider what language to pick when building systems? It is mostly about the purpose of the system, and what we bet on. I tend to bet on the culture and the community behind the language. (of course, there are also economical aspects, but I am not going into there)

#### Static vs Dynamic Typing

Dynamically languages are known to be very useful and expressive, but not as safe as the statically typed languages. When these terms are discussed, people usually confuse this with strong vs weak typing. But dynamically typed languages can very well be strongly typed (e.g. python). In the past, dynamic languages were used more often in web development.

But modern statically typed languages catch up on the productivity as the compiler technologies evolved dramatically in the last 10 years. Though, they are still not there yet. Rust, Kotlin, C# are good examples of this. They are not as verbose, and can make clever assumptions on typing (e.g. implicits).

On the other hand, dynamically typed languages also saw the usefulness and the demand from the communities to include strong typing integrated into the languages. That's why javascript (with typescript) and python added [gradular typing](https://en.wikipedia.org/wiki/Gradual_typing) feature into the languages. Though, they don't benefit from the performance benefits of static type systems in statically typed compiled languages.

It is easy to build systems in dynamic languages. But if I ever hear "easy", I start questioning things for the consequences.

**Easy != Simple**

<figure>
    <img src="https://imgs.xkcd.com/comics/python.png" height="400px">
    <figcaption><a href="https://xkcd.com/353/">[image from xkcd]</a></figcaption>
</figure>

#### FP vs OOP

Not gonna lie, I am a fan of FP. Even though OOP helps a lot on modelling the real-world application business logic, it also leads to "unsafe" programming as it encourages stateful programming. This becomes a big issue when dealing with concurrency related problems. It is inherently hard to deal with concurrency problems, so it is best to avoid them.


### Having a good taste

![good taste or me](/images/good-taste-or-me.jpg)

It is debatable whether there is such thing as good taste or not. Is it really _that_ subjective? Just because we can't express a subject formally in a language (e.g. mathematics) does not mean the subject is purely subjective. That may very well mean we just couldn't come up with the formality with those concepts yet. Though subjects like favorite color, music, cousine may have tight coupling on interpretation with your past memories and experiences are out of this discussion.

Historically, a paradigm considered as good might be considered bad practice in the future. And popularity of a paradigm or methodology is not correlated with the good taste.

Douglas Crockford once said;

> - It took a gene­ra­tion to agree that high level lan­gua­ges were a good idea.
> - It took a gene­ra­tion to agree that goto was a bad idea.
> - It took a gene­ra­tion to agree that objects were a good idea.
> - It took two gene­ra­ti­ons to agree that lamb­das were a good idea.

Linus Torvalds -if we can ignore his ego- has a reference to good taste in programming [in one of his talks][torvalds-good-taste]. Also, Paul Graham discusses the subject in [this article][good-taste].


## Software Engineering

The field of software engineering is still in early stages. In the late 80s, one of the most influencal people in Computer Science, [Gerald Sussman](https://en.wikipedia.org/wiki/Gerald_Jay_Sussman) foresaw that programming is same as geometry of the ancient greek times. Back then, he stated that we are living in an era where we just discovered it, but we will realize the importance and usefulness of programming in the future to build systems. This was a very bold statement during that time. He almost knew, in 40 years ago, we were going to have a software-defined world.

So where is software engineering now, when we are talking about the software systems? Do software engineers apply science? Is it math? Some wizardry? engineering? My answer is;

- There is wizardry on having beautiful abstractions, elegancy in the code, clever ingenious solutions.
- There is engineering for optimizing the trade offs on both human (engineer time) hardware (where does it run, allocation), software (the entire stack is full of trade offs) resources.
- There is science when we reason about the system's SLA, handling load, resources capabilities, performance analysis
- And lastly... there is math in all of the above.


[good-taste]: http://www.paulgraham.com/goodtaste.html
[torvalds-good-taste]: https://youtu.be/o8NPllzkFhE?t=856