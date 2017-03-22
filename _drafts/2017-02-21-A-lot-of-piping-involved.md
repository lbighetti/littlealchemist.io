---
layout: post
title: A lot of Piping involved
date:   2017-02-21 16:39:00 +0100
---

Let's learn about a core feature of Elixir and many other functional languages: it's called __piping__.

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

```
output1 = function(param)
output2 = function2(output1, foo)
output3 = function3(output2, bar)
output4 = function4(output3, supa, dupa)
```

Or... more interestingly:

```
output4 = function4(function3(function2(function(param), foo), bar), supa, dupa)
```

_(Do you even code readability brah?)_

Now we cast the _pipe spell_ on it:

```
param
  |> function
  |> function2(foo)
  |> function3(bar)
  |> function4(supa, dupa)
```

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
