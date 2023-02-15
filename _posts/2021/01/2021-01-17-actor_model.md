---
title: "Actor model"
excerpt: "A mathematical model of concurrent control"
toc: true
toc_sticky: true
published: true
# header:
#   teaser: /assets/images/2021/01/17/supervisor_actor.png
#   image: /assets/images/2021/01/17/supervisor_actor.png
#   caption: "Photo by me"
#   og_image: /assets/images/2021/01/17/supervisor_actor.png
layout: single
# classes: wide

categories:
    - Rust
tags:
    - Concurrent
last_modified_at: 2021-01-17T08:06:00-05:00
---

# Intro 
Following a roadmap [[1]](#first) to study about web application using Rust, I find [Actix](https://actix.rs/) framework. On the homepage, it says it's an "actor" framework. I have no idea what the "actor" means. According to Wikipedia [[2]](#second), the actor model is a mathematical model of concurrent control. Let's try to dig it more and way to understand.

# Actor model 
## <a name="pure_function">Pure function</a>
Have you heard about a pure function? I faced this term when I tried to learn [Scala](https://www.scala-lang.org/) language. The pure function returns the same result if inputs are the same, and it creates no side-effect. Since a snippet of source code produces the same value, it is possible to use it in a distributed system. We can get whatever we expect without a careful design of the concurrency control because there is no global-level modification by default. 

## Erlang 
![supervisor_and_actor](/assets/images/2021/01/17/supervisor_actor.png)

In the real world, [Erlang](https://www.erlang.org/) is one famous language that implements the actor model. [[3]](#third) I remembered the first time I met the Elixir. The philosophy of Elixir is "let it crash!". It is not familiar with the other languages. In Elixir, I need to design one supervisor that can handle an invalid scenario. Using the invalid handler, we can relaunch the app when it faces an invalid situation. It means it can be self-healed from an error. 

## Actor
I understand that "Actor" works like the [pure function](#pure_function) with more functions. It has a message queue and processes the message in a FIFO(First In First Out) way. The actor does three operations; 
* Create more Actors 
* Send messages to other Actors 
* Designate what to do with the next message 


# Outro 
In this short post, I try to explain what the actor model is. For me, the name of it is close to the "executor". While I'm writing this article, I can look back on Scala and Elixir. Thank you, and please leave messages if I'm wrong. 

# Reference
<a name="first">[1]</a> [https://github.com/anshulrgoyal/rust-web-developer-roadmap](https://github.com/anshulrgoyal/rust-web-developer-roadmap)

<a name="second">[2]</a> [https://en.wikipedia.org/wiki/Actor_model](https://en.wikipedia.org/wiki/Actor_model)

<a name="third">[3]</a> [https://www.brianstorti.com/the-actor-model/](https://www.brianstorti.com/the-actor-model/)