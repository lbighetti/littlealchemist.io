---
layout: post
current: post
navigation: True
title: Exploring Kotlin
tags: kotlin
class: post-template
subclass: 'post tag-kotlin'
author: leandro
excerpt: Exploring Kotlin
meta-description: Exploring Kotlin
cover: False
---

# Exploring Kotlin

## Overview?

## Installing

- mac `brew install kotlin`
- linux ?
- windows ?

## REPL (iex-like)

Because I've been using elixir for the last 2 years I got really used to developing using `iex` my first idea was to check if there is anything similar in Kotlin, and it turns out it does.

The way you access it is by running the compiler with no argument:

```bash
> kotlinc
```

Then you can test Kotlin code in real time.

Funny enough the [docs page](https://kotlinlang.org/docs/tutorials/command-line.html) doesn't include how to quit 😂 and I got stuck in a vim-fashion wise. However it's easy enough, if you want to leave:

`:quit`

## Testing the basics

### Numbers

Thought I'd start by trying out some basic math:

```kotlin
>>> 1 + 2
res0: kotlin.Int = 3
>>> 1 / 2
res1: kotlin.Int = 0
>>> 1 - 2
res3: kotlin.Int = -1
>>> 1 * 2
res4: kotlin.Int = 2
>>>
```

Nothing too unexpected, except the division returning `Int`. I'm guessing as Kotlin is statically typed it must be infering the results type from the arguments. And sure enough, forcing it with a decimal point gets us the non-integer response:

```kotlin
>>> 1.0 / 2.0
res2: kotlin.Double = 0.5
```


----- 

## Another post

# Gradle with Kotlin for Elixir's mix-like capabilities

