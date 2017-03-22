---
layout: post
title: Understanding Elixir Pattern Matching
date:   2017-03-15 20:00:00 +0100
image: /img/elixir_pattern_matching.png
share-img: /img/elixir_pattern_matching.png
excerpt: Let's understand what is Pattern Matching in Elixir and how it makes code more efficient and more readable.
meta-description: Let's understand what is Pattern Matching in Elixir and how it makes code more efficient and more readable.
---
I had heard about Pattern Matching before and was totally clueless about it. But when I started learning Elixir it soon struck me: __the equal sign works differently__.

Usually, in programming the __equal sign__ performs an __assignment__.

So if you have a expression like:

```elixir
foo = 7
```

Would usually mean you're __evaluating__ the expression on the right, and are __storing__ the result in the variable on the left.

```elixir
foo = ["b", "a", "r"]
```

Here for instance, most languages will consider this list on the right an entity `["b","a","r"]` and will store this entity (or reference to it) in the variable on the left - `foo`.

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

In the first example Elixir would bind the variable __foo__ to `7`.

```elixir
foo = 7
```

In the second example, foo would bind to the list `["b", "a", "r"]`

```elixir
foo = ["b", "a", "r"]
```

However, this would also work:

```elixir
[foo, bar, ho] = ["b", "a", "r"]
```

Yes.  
__foo__ binds to `"b"`, __bar__ binds to `"a"` and __ho__ binds to `"r"`.

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

## And what happens when the match fails ?

In the above case, the match will fail. Because as mentioned, Elixir cannot bind the values on the left to `foo`.  
In this case, a __Match Error__ will be raised.

>** (MatchError) no match of right hand side value: 7

This means Elixir was unable to match what you told it to.  
Bad, bad match!

## More examples

Another thing you can do is match when the data structure carrying different data types.  
For example:

```elixir
[a, b] = ["foo", 42]
```

As you can imagine, __a__ bind to `"foo"` and __b__ to `42`.

You can even match a list within a list.

```elixir
[a, b, c] = ["foo", 42, ["hello","little", "alchemist"]]
```

And besides __a__ and __b__ continuing as before, now __c__ will bind to `["hello","little", "alchemist"]`.  
And you can even go one step futher and do:

```elixir
[a, b, [c, d, e]] = ["foo", 42, ["hello","little", "alchemist"]]
```

And now __c__,__d__ and __e__ will bind to `"hello"`, `"little"` and `"alchemist"` respectively.

## Maps

One very common thing to do in Elixir is pattern match Maps, which is super powerful.

This is how you define a map in Elixir:

```elixir
%{"key" => "foo"}
```

Coming from java this was a weird syntax, so take your time to process it if you've never seen it before.  
It's simple, it means the string `"key"` is a key in your map, and retrieving it will get you the value `"foo"`.

Now, back to the pattern matching, you can obviously bind this to a variable:

```elixir
my_map = %{"key" => "foo"}
```

And also, as mentioned, retrieve the value `"foo"` into a variable similarly:

```elixir
my_value = my_map["key"]
```

>foo

But here it comes:

```elixir
%{"key" => my_value} = %{"key" => "foo"}
```

Here the map on the left has to equal the map on the right.  
For this to happen, __my_value__ needs to equal `"foo"`, and that's precisely what happens.

For pattern matching to work on __maps__, the __keys need to match__ - which is happening here.  
So Elixir binds the value on the left, to the value on the right.

And you can even do this storing the map on a variable:

```elixir
my_map = %{"key" => "foo"}
%{"key" => my_value} = my_map
```

Here, __my_value__ will still bind to `"foo"`.  
Elixir try to make the maps on both side match. So as long as the keys match, it will bind the _value on the left_ (__my_value__), to the _value on the right_ `"foo"`.

In other words, it has the same effect as doing this:

```elixir
my_value = my_map["key"]
```

As long as the key of the map match, you can use variables as you please - just keep in mind that again, only the left side will be able to bind variables.


## The Pin Operator ^

Say you want to match the __value stored within your variable__.  
When you would like to put the variable on the left, but you _don't want Elixir to bind it to something else_.

In this case you can use the __pin operator__: `^`.
Then, you can __match using value stored within the variable, not as a normal variable__.

```elixir
foo = 3
[^foo, bar] = [3, "awesome"]
```

Let's understand what this means.  
This will match when __foo is already equal to 3__. It will not match when foo it is not 3, and it __will not bind foo to 3__.

This, for instance, will raise an Error:

```elixir
foo = 3
[^foo, bar] = [5, "not good"]
```

>** (MatchError) no match of right hand side value: [5, "not good"]

---

Cool. Now process all of this and take a moment, because we have one last trick. And it's tricky.

## Pattern Matching a Map on function argument

This is my favourite.

You have a function, and you receive __a map as an argument__.
And you need the value that comes from the key `"foo"`.

```elixir
my_map = %{"foo" => "bar"}
my_function(my_map)
```

Let's say you want to define this `my_function`. You want that to print the value stored on the key `"foo"` from the argument map.  
How to achieve this ?

You can do this like so:

```elixir
def my_function(%{"foo" => my_variable}) do
  IO.puts my_variable
end
```

Now if we go ahead and pass in a map to your function, it's gonna retrieve the right value:

```elixir
my_map = %{"foo" => "bar"}
my_function(my_map)
```

> "bar"

_Boom! Headshot!_

---

That's it for today!
A very interesting topic and I will surely further expand on another post in the future.

Hope you enjoyed it,
Don't forget to like the post and share with your friends - It's only fair to share!

And until next time,
Take care and happy brewing!
