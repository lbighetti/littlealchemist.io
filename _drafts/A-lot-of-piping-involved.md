---
layout: post
title: A lot of Piping involved
---

Let's learn about a core feature of Elixir and many other functional languages: it's called __piping__.

When I decided to jump into Elixir, I had a dialog with a good german friend of mine (Robert if you're reading, you're awesome).

It went something like this:
Me: _I'm going to work with Elixir._
Him: _Elixir? ...mkey...never heard of it._
Me: _It's a functional language that runs on the Erlang VM_
Him _Functional? There will be a lot of piping involved._

Wise man.  
There is indeed.

This is how it looks like:

```
|>
```

Time for some plumbing.

But actually it's more like a factory.
Let me explain.

The __pipe__ is used to make __sequential transformations__ much more readable.

Imagine you need call a function with a certain parameters you have, and use the output of that as argument to call a second function. Like so:

```
output1 = function(param)
```

Now, often you have to to this multiple times in sequence, making something like this :

```
output1 = function(param)
output2 = function2(output1)
output3 = function3(output2)
output4 = function4(output3)
```

Of course you can tell me, I can simplify that in most languages to:

```
output4 = function4(function3(function2(function(param))))
```

Now, let me tell you, that's not very readable, is it ?

What's worse, you have to read this code from left to right then switch to right to left, and read it inside out.
That's not the natural orders we humans read things.

We are simple beings.
We see code like this, we get confused.

Here is how you would do that in Elixir:

```
param
  |> function
  |> function2
  |> function3
  |> function4
```
