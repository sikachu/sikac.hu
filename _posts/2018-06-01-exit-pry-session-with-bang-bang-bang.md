---
layout: post
title: A faster way to exit a Pry session
date: 2018-06-01T14:01:01.970Z
original: d05f15f244ce
---

If you are using Pry in your project,
you might run into a situation where you are in a loop or
have multiple `binding.pry` calls
so you have to use exit multiple times to get out of it.

So, instead of using `exit` multiple times,
you can use `exit-program` to continue the execution
without breaking into Pry again.

There is also a handy shortcut for this, which is `!!!`.

You can read more about `exit-program`
and other ways to navigate around in your Pry session
in [Pry's wiki page].

[Pry's wiki page]: https://github.com/pry/pry/wiki/State-navigation#exit-the-program-completely
