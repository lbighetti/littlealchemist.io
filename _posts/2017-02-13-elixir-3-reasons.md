---
layout: post
title:  "Elixir - 3 reasons why you should be using it"
date:   2017-02-13 14:12:00 +0100
categories: elixir
---

## Reason 1: Functional

* _Elixir is a proper functional language._

And why is this a good thing ?

Because the problem of a __web server__ is a very __functional one__.

Think about it for second.

You receive a request, do something, and then you produce a response.  
You receive a very defined input, and produce a very defined output.

__It's a function.__

You see, _the nature of the problem is functional_, so it only makes sense to use a functional language to solve it.

But that's not all.

__Data immutability.__

In Elixir, all data is immutable.  
This means your data is safe from being changed by some other part of your application or by some other application.

Sure, you can still _bind_ your variable to another value, but the value itself is immutable.

Imagine that, _the end of concurrency nightmares._

## Reason 2: Erlang

* _Elixir runs on the Erlang VM, and is fully interoperable with Erlang._

Let me tell you something about Erlang.

It's fast.

It's extremely fault-tolerant and scalable.

In Erlang, all memory and CPU cores available are used to it's maximum potency.  
More importantly, it runs tiny tiny Erlang processes which _are not_ system processes.  
They are much smaller and more lightweight.

Erlang will execute it's tiny processes using all cores and memory available.  
Consequently, two extremely awesome things happen:

_the end of your multi-threading and scalability nightmares_.

And not with some rocket science setup, this all works out-of-the-box.

Now, let's go through some real world facts about Erlang.

It runs more than 50% of all telecom systems on the planet.  
How often is your landline telephone "down", or "temporarily unavailable" ?

Not very often is it?

Another major project using Erlang is the real-time chat application WhatsApp.  
When Facebook bought them, they were running _millions of connections in a single Erlang node_.

Enough said.

## Reason 3: Phoenix

* _Phoenix is the de facto web framework for Elixir and it's awesome._

Let's assume you believe me so far.

You might reason as follows:

"OK Leandro, cool, we have a language that is fast, reliable, fault-tolerant and easy to distribute in a mountain of cores and servers. Great.

But I have kids to feed. I have to pay my rent, pay my taxes, so...

__Is it productive ?__

Can I quickly - and effectively - create a new web project, whether it is a rest API or fullstack ?

This talk is great, but X, (replace X with great language + framework combos: Spring Boot / Rails, Django, Play...) X allows me to achieve higher orders of productivity because they already solve most of common problems for me and perform the usual setup automatically. I just modify to my taste and focus on my logic.

How can I possibly achieve this here ? "

I know.

I have asked myself the same question.

The answer is __Phoenix.__

Reborn from flames and ashes. Again and again.  
It will not die.

Ever.

Phoenix is your go-to web framework in Elixir.  
Phoenix was designed with lessons learned from decades of web development.  
It comes with great support for building rest APIs, sockets and full stack applications.

It's awesome.

You can generate projects with one command and a prototype within minutes.  
You can have a potent frontend with the Elixir template engine.

Or you can make beautiful and stupidly fast rest APIs and sockets.

Or both.
You choose.

Whatever web application you need to build, Phoenix has got you covered.

---

To recap:

* Functional - great for webserver, concurrency.
* Erlang - Fault-tolerant, Scalable and mature.
* Phoenix - Fast, Productive, reliable.

In a nutshell, those were the main points for my decision to jump onto Elixir.

---
Don't forget to like this post and share it with your friends.

I hope you enjoyed, I'll see you next time.  
Take care,
