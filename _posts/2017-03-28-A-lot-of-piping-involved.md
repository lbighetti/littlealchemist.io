---
layout: post
title: A lot of Piping involved
date:   2017-03-28 15:00:00 +0100
---

Let's learn about a core feature of Elixir and many other functional languages: it's called __piping__. Then we'll go over a real world example of how to utilize it.

When I decided to jump into Elixir, I had a dialog with a good german friend of mine (Robert if you're reading, you're awesome).

It went something like this:  
Me: _I'm going to work with Elixir._  
Him: _Elixir? ...mkey...never heard of it._  
Me: _It's a functional language that runs on the Erlang VM_  
Him: _Functional? There will be a lot of piping involved._  

Wise man.  
There is indeed.

This is how it looks like:

```elixir
|>
```

Time for some plumbing.

But actually it's more like a factory.  
Let me explain.

The __pipe__ is used to make __sequential transformations__ much more readable.

Imagine you need call a function with certain parameters you have, and use the output of that. Like so:

```elixir
output1 = function(param)
```

Now, often you have to to this multiple times in sequence, making something like this :

```elixir
output1 = function(param)
output2 = function2(output1)
output3 = function3(output2)
output4 = function4(output3)
```

Of course you can tell me, I can simplify that in most languages to:

```elixir
output4 = function4(function3(function2(function(param))))
```

Now, let me tell you, that's not very readable, is it ?

What's worse, you have to read this code from left to right then switch to right to left, and read it inside out.  
That's not the natural orders we humans read things.

We are simple beings.  
We see code like this, we get confused.

Here is how you would do that in Elixir:

```elixir
param
  |> function
  |> function2
  |> function3
  |> function4
```

## Oh cool! Wait... what just happened?

It's pretty straight-forward.

Whatever the __output__ of the function being called, it will be __passed to the next function as a argument__.  
And the argument of your first function is the thing on the top, in this case _param_.

So if we wanna break it down, for explanation sake, we could write it like:

```elixir
output =
  param
    |> function
```

That's the same as writing:

```elixir
output = function(param)
```

For just 1 function like this, it probably doens't make much sense to pipe.

Progressing to two function calls:

```elixir
output2 =
  param
    |> function
    |> function2
```

The above is the same as:

```elixir
output = function(param)
ouput2 = function2(output)
```

or more shortly:

```elixir
ouput2 = function2(function(param))
```

So...

Hopefully you can see now how this:

```elixir
output4 = function4(function3(function2(function(param))))
```

Is the same as the piped counterpart:

```elixir
param
  |> function
  |> function2
  |> function3
  |> function4
```

And hopefully you can see how much more readable that is :)

## But I need more Oomph!

_"Great Leandro, but my real world problems don't look like that.  
Clearly my functions have **several arguments**, not just one.  
How does your piping-schmiping handle that?_

No sweat.  
You can add arguments on the function calls.

Just remember, __the first arguments is always the previous output__.

So how would it look like?
Let's imagine that instead, you have these function calls:

```elixir
output1 = function(param)
output2 = function2(output1, foo)
output3 = function3(output2, bar)
output4 = function4(output3, supa, dupa)
```

Or... more interestingly:

```elixir
output4 = function4(function3(function2(function(param), foo), bar), supa, dupa)
```

_(Do you even code readability brah?)_

Now we cast the _pipe spell_ on it:

```elixir
param
  |> function
  |> function2(foo)
  |> function3(bar)
  |> function4(supa, dupa)
```

## A Brief Conceptual Thought

Programming should be about __transforming data.__  
Yes, you input stuff and you output stuff.

In, and out.  
It's simpler when we think about it this way, and it is what functional programming is all about.

Another way to imagine is that you have a series of __transformations__.

Another way to write the above code would be like:

```elixir
param |> function |> function2(foo) |> function3(bar) |> function4(supa, dupa)
```

See ?  
It's like production line.



## Real-world-shit time

Ok, now let's __actually__ achieve something other than raving about this.

Let's say you have the following scenario: __a list of emails, separated by commas.__  
And that you want to do the following to it:

1. Force all emails to be __lowercase__
1. __Separate__ them into a __list of strings__
1. __Remove duplicates__

Let's quickly go over the Elixir functions we'll need for this:

```elixir
String.downcase/1
String.split/2
Enum.uniq/1
```

Just in case you don't know, Elixir signature of functions are defined only by their __arity__. That is, the __amount of arguments it receives__.

In this particular case the `String.downcase/1` and `String.split/2` receive the __target string as the first argument__ and `String.split/2` also receives the separator as the second argument.

`Enum.uniq/1` receives a enumerable and removes all duplicates.

Say the string we want to transform is in a variable named `input`:

```elixir
input = "Example@Gmail.com,ExamplE@Gmail.COM,anoTHER.example@GMAIL.com"
```
__Note the first two emails are duplicates.__

Let's start with a yet different trick to piping, which is, __we can put the string alone__ in the first line:

```elixir
input
  |> String.downcase
```

>"example@gmail.com,example@gmail.com,another.example@gmail.com"

This is the same as calling `String.downcase(input)`.  
Let's evolve it one more step.

```elixir
input
  |> String.downcase
  |> String.split(",")
```

>["example@gmail.com", "example@gmail.com", "another.example@gmail.com"]

And, __alas__.

```elixir
input
  |> String.downcase
  |> String.split(",")
  |> Enum.uniq
```

>["example@gmail.com", "another.example@gmail.com"]

P R O P E R L Y.

O N  
A  
D A I L Y.

---

That's it for today, hope you enjoyed it.

Don't forget to _like_ and share this post with your friends and anyone interested in learning about this subject.

If this was useful to you,  
please leave a comment and let me know!

If it wasn't, also leave a comment and point out what a total crap and waste of your time it was.

Take care and until next time,
Happy brewing!
