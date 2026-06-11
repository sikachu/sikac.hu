---
layout: post
title: How to keep sensitive commands out of .zsh_history
date: 2015-11-09T01:49:01.921Z
original: 29a2f39ae17f
---

By default,
if you enable command history in Zsh,
all commands including those that contain sensitive information
such as an access token or a password
will be saved into your command history file after you run them.

It’s definitely a bad idea to have that information
wound up in your `.zsh_history` file.

However,
there is a way you can tell Zsh to not putting a command in your history file
by setting this option in your `.zshrc`:

```zsh
setopt HIST_IGNORE_SPACE
```

After that,
Zsh will not store any command that starts with a space in a history file.

So, instead of running this:

```
$ curl -u "LOLNOPE:x-oauth-basic" -i https://api.github.com/...
```

add an empty space before your command like this:

```
$  curl -u "LOLNOPE:x-oauth-basic" -i https://api.github.com/...
  ^--------- notice an empty space here
```

Note that this most recent command _will_ temporarily stay in the command history
in your current session
so you can go back to reuse or edit it by using the UP arrow,
and it will automatically disappear
after you run another command in the same session.

You can read more about this in [Zsh documentation](https://zsh.sourceforge.io/Doc/Release/Options.html)
