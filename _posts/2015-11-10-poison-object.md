---
layout: post
title: "Poison Object: An Antidote for Your Nil"
date: 2015-11-10T14:09:15.958Z
original: "14ea60e8fe84"
---

I recently submitted a [pull request] to Ruby on Rails
to make force reloading an association more explicit.
I then came across this [suggestion] from [Sage Griffin]:

> Rather than using *nil* here, can we be a little bit more explicit?
> A user could have theoretically been passing *nil* here,
> since we were just relying on truthy/falsy.

The code that they commented on looked like this
(notice the `force_reload = nil` default):

```ruby
def reader(force_reload = nil, reload: false)
  # Override `reload` if user passed in `force_reload`
  unless force_reload.nil?
    reload = force_reload
  end

  if reload
    # Executing code to reload the association
  end
end
```

They proposed that instead of using *nil* as a default value,
I should create a *poison object* instead.
My code now looked like this:

```ruby
NO_FORCE_RELOAD_ARGUMENT = Object.new

def reader(force_reload = NO_FORCE_RELOAD_ARGUMENT, reload: false)
  if force_reload != NO_FORCE_RELOAD_ARGUMENT
    reload = force_reload
  end

  if reload
    # Executing code to reload the association
  end
end
```

This way, if a user passes in *nil* as an argument,
the code will properly set the *reload* argument to *nil*
instead of leaving it at the keyword argument’s value.

---

Next time you use *nil* as a default argument,
don’t forget to ask yourself a question:

*“Do I actually want to check whether the user passed in an argument?”*

If you do, consider using a poison object like the example above.
It will make your code much clearer.

[pull request]: https://github.com/rails/rails/pull/20883
[suggestion]: https://github.com/rails/rails/pull/20883#discussion_r34624606
[Sage Griffin]: https://github.com/sgrif
