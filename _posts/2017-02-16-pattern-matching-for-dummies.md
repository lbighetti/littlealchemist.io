---
layout: post
title: Pattern Matching for Dummies
date:   2017-02-16 19:29:00 +0100
---
I started learning Elixir and it soon struck me: __the equal sign works differently__.

Usually, in programming the equal sign performs an __assignment__.

So if you have a expression like:

```elixir
foo = 7
```

Would usually mean you're evaluating the expression on the right, and are storing the result in the variable on the left.

```elixir
foo = ["b", "a", "r"]
```

Here for instance, most languages will consider the array on the right an entity, and will store this entity (or reference to it) in the variable on the left.

Sounds reasonable right ?

__This is not how it works in Elixir.__

## The Equal Sign In Elixir

In Elixir (and in Erlang) the __equal sign__ performs a __pattern matching__ operation.

What is pattern matching ?

It is just as the name implies.  
Elixir will try to make the expressions on both sides be equal.

In different words: it will make whatever it can so that things on the left can equal the things on the right.

__This is not limited to 1 variable__.

In the above case it would still work mostly as you imagine, with a slightly different naming, it is called __variable binding__.

In the first example Elixir would bind the variable __foo__ to __7__.

In th second example, foo would bind to the array `["b", "a", "r"]`

However, this would also work:

```elixir
[foo, bar, ho] = ["b", "a", "r"]
```

Yes.
__foo__ binds to _b_, __bar__ binds to _a_ and __ho__ binds to _r_.

Awesome, isn't it ?

Similarly:

```elixir
["b", bar, ho] = ["b", "a", "r"]
```

## Left Wing matching

Elixir will only bind variables on the __left__ side though.

So for instace, if you do this in sequence:

```elixir
foo = 7

foo = ["b", "a", "r"]
```

This will work fine.

However, this will not:

```elixir
foo = 7

["b", "a", "r"] = foo
```

Since now foo is 7 and it is on the right, Elixir will not bind it to something else.

## Maps

One very common thing to do in Elixir is pattern match Maps, which is super powerful.

This is how you define a map in Elixir:

```elixir
%{"key" => "value"}
```

Now you can obviously bind this to a variable:

```elixir
a = %{"key" => "value"}
```

But here it comes:

```elixir
%{"key" => b} = %{"key" => "value"}
```
Here, __b__ is now _value_.

And you can even do this, which has the same effect:

```elixir
a = %{"key" => "value"}
%{"key" => b} = a
```

Here, __b__ is still _value_.

As long as the key of the map match, you can use variables as you please - just keep in mind that again, only the left side will be able to bind variables.

## Pattern Matching a Map on function argument

This is one of my favourite tricks.

Now you have a function, and you receive a map as an argument.
And you need the value that comes from the key `"foo"`.

You can achieve this like so:

```elixir
def my_function(%{"foo" => my_variable})
  IO.puts my_variable
end
```

Now if we go ahead and pass in a map to your function, it's gonna retrieve the right value:

```elixir
my_map = %{"foo" => "bar"}
my_function(my_map)
```

In this case, it will print

> "bar"

---

That's it for today, a brief description of pattern matching in Elixir and how to use it.  
A very interesting topic and I will surely further expand on another post in the future.

Hope you enjoyed it,

And until next time,
happy brewing!
