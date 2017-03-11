Elixir - What are these Tuples Schmuples anyway ? And Atoms ? Atomic Tuplewares ?
or The Atomic Tuppleware - a brief tale about Tuples and Atoms.

In Elixir there is a data structure called Tupple. What a funky name. Reminds me of tupperware. There is also a data type called Atom. Let's go over what they are, how they're used in Elixir and why they're powerful.

## Chapter 1: Tuples.

I was watching a video from José Valim at Pluralsight, and I heard him say that a function would return a __Tuple__.

I had never heard that word before.

Tuple.

TuppleTuppleTupple.

Ha!

It's  a funky name isn't it ?

There is a weird sound to it.

_TUPLE._

Anyway he went on to show something really cool.  
The function he was mentioning returning something like this:

```elixir
{:ok, result}
```

Okay, I thought, that looks interesting.  
It's like you have this __first piece__ which tells you __if the outcome was good or bad__, _and then_ you get your so desired result.

Similarly, the function could otherwise return:

```elixir
{:error, reason}
```

Damn, neat!  
Isn't it ?

But then... he said the first item was an __atom__.

Atom ?
__An ATOM?__

__What the hell is an atom ??__

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

They are especially useful when used mostly internally in your application but not necessarily printed.  
So instead of saying your function went `"ok"` as a string, you say that it went `:ok`, as an atom.

This is probably natural for Rubists but me coming from Javaland it was totally alien.

`:ok`, back to the __tuples__.

## Back to Chapter 1: Tuplewares

Right, so, now I get what `:ok` and `:error` are supposed to do there.  
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
By the way check out my [Pattern Matching post](<<link>>) if you haven't yet.  
Go, I'll wait.

Now, let's say this function that returned the tuple is called like `your_function(argument)`.

Typically we would then do something like this:

```elixir
case your_function(argument) do
	{:ok,  result} ->
		# do successful stuff
	{:error, reason} ->
		# do erroneous stuff
end
```

Damn.  
Tell me that's not beautiful.

It's no the only way that this is used though.  
Another example would be something like the Ecto.update_all/3

This function returns a tuple also, but it's a little different.  
This function is updating several rows ina a database, so what the return tuple gives is `{rows_affected, output}`, and if there is no output, it simply comes `nil`.

So if you updated there and you updated 57 rows, and the database returned no output, it would throw you this:

```elixir
{57, nil}
```

Again, loyal.  
Properly saluted!

## Epilogue

So that's my brief memoir of Tuples and Atoms.  
Hope you enjoyed, don't forget to like the post and share with your friends.

Until next time,
Take care and happy brewing,
