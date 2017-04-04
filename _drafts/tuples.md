---
layout: post
title:  "Understanding Tuples and Atoms in Elixir"
date:   2017-04-05 15:50:00 +0100
image: /img/elixir.png
share-img: /img/elixir.png
category: elixir
excerpt: Let's go over what are Atoms and Tuples, how they're used in Elixir and why they're powerful.
meta-description: Let's go over what are Atoms and Tuples, how they're used in Elixir and why they're powerful.
---
<!-- or The Atomic Tuppleware - a brief tale about Tuples and Atoms. -->
In Elixir there is a data structure called __Tuple__. What a funky name.
<!-- Reminds me of tupperware. -->

There is also a data type called __Atom__.  
Let's go over what they are, how they're used in Elixir and why they're powerful.

## Chapter 1: Tuples.

I was watching a video from José Valim at Pluralsight, and I heard him say that a function would return a __Tuple__.

I had never heard that word before.

Tuple.

_TuppleTuppleTupple._

Ha!

It's a funky name isn't it ?

There is a weird sound to it.

_TUPLE._

Anyway he went on to show something really cool.  
The function he was mentioning returned something like this:

```elixir
{:ok, result}
```

_Okay_, I thought, _that looks interesting_.  

It's like you have this __first piece__ which tells you __if the outcome was good or bad__: `:ok`, _and then_ you get your so desired `result`.

Similarly, the function could otherwise return:

```elixir
{:error, reason}
```

Damn, neat!  
Isn't it ?

But then... he said the first item was an __atom__.

_An ATOM?_

_What the hell is an atom ??_

I mean, I know what an atom is, but I'm guessing this isn't the kind that has electrons and neutrons.

## Chapter 2: Atoms

I went to Elixir website:

>Atoms are constants where their name is their own value. Some other languages call these symbols.

```elixir
iex> :hello
:hello
iex> :hello == :world
false
```

>The booleans true and false are, in fact, atoms:

```elixir
iex> true == :true
true
iex> is_atom(false)
true
iex> is_boolean(:false)
true
```

Ah!
Ok, so, atoms are like symbols.
__Symbols that carry a meaning.__  
And the Erlang virtual machine only keeps 1 copy of each atom in memory.

They are especially useful when used internally in your application but not necessarily printed.  
So instead of saying your function went `"ok"` as a string, you say that it went `:ok`, as an atom.

This is probably natural for Rubists but me coming from Javaland it was totally alien.

A good property of an __atom__ is that it is __universal and equal__ even between different machines.  
So an `:ok` will be equal to another `:ok`, even if they're in different servers or Erlang nodes.

`:ok`, back to the __tuples__.

## Back to Chapter 1: Tuplewares

So, now I get what `:ok` and `:error` are supposed to do there.  
The first item on the tuple tells me what happened, and the second gives me the details.

But let's talk about the tuples a little more.

What are Tuples?  
__Tuples are a collection of values.__  
They typically come in the size of 2 or 3 items, so small, not your collection to store life stories and your bank statement, but more of like summary information.

The way I showed you, is one of the most common ways it is used in Elixir.

```elixir
{:status_atom, your_stuff}
```

And what do functional programmers do ?

That's right.

We Pattern Match!!  

## Case and Pattern Matching with Tuples

Let's talk briefly about `case` in Elixir.
By the way check out my [Pattern Matching post](<<link>>) if you haven't yet.

```elixir
case number do
	1 -> IO.puts "Number one"
	2 -> IO.puts "Number two"
	_ -> IO.puts "Something other than one or two"
end
```

This is how we use case in Elixir.  
You put a expresion, variable or function call __right after the case__, and put options to control the flow of the program.

When `number` is equal to `1`, the program will print `"Number one"`.
Likewise, when it is `2`, `"Number two will be printed"`.  
Anything else will get you the `"Something other than one or two"` option.

Note that the `_` matches to anything, and the __underscore__ itselftdenotes that we _don't intend to use this value at all_.  
We basically don't care about the value in this case.

Now, let's say we have this function: `your_function(argument)`, that we know returns a tuple.

Typically we could do:

```elixir
case your_function(argument) do
	{:ok,  result} ->
		# do successful stuff
	{:error, reason} ->
		# do erroneous stuff
end
```

What this means is:

1. Call `your_function` passing the parameter `argument`.
1. Analyse the result returned by `your_function(argument)`
1. Choose whether the result looks like `{:ok, something}` or `{:error, reason}`
1. Follow the appropriate course of actions, based on the previous assessment.

Damn.  
That's beautiful.

You avoid putting a lot of boilerplate code to support straight forward use cases.  
And also very complicated ones actually.

However, this is not the only way __tuples__ are used.  
Another example would be something like the `Ecto.update_all/3`.

This function returns a tuple also, but it's a little different.  
This function is updating several rows ina a database, so what the return tuple gives is `{rows_affected, output}`, and if there is no output, it simply comes `nil`.

So if you updated there and you __updated 57 rows__, and the database returned __no output__, it would give you this:

```elixir
{57, nil}
```

Again, loyal.  
Properly saluted!

## Epilogue

So that's my brief memoir of Tuples and Atoms.  
Hope you enjoyed, don't forget to share this post with your friends.

And until next time,
Take care and happy brewing,
