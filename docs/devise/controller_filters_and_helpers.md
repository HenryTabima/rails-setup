---
id: controller-filters-and-helpers
title: Controller filters and helpers
---

Devise will create some helpers to use inside your controllers and views. To set up a controller with user authentication, just add this before_action (assuming your devise model is 'User'):

```ruby
before_action :authenticate_user!
```

For Rails 5, note that `protect_from_forgery` is no longer prepended to the `before_action` chain, so if you have set `authenticate_user` before `protect_from_forgery`, your request will result in "Can't verify CSRF token authenticity." To resolve this, either change the order in which you call them, or use `protect_from_forgery prepend: true`.

If your devise model is something other than User, replace "_user" with "_yourmodel". The same logic applies to the instructions below.

To verify if a user is signed in, use the following helper:

```ruby
user_signed_in?
```

For the current signed-in user, this helper is available:

```ruby
current_user
```

You can access the session for this scope:

```ruby
user_session
```

After signing in a user, confirming the account or updating the password, Devise will look for a scoped root path to redirect to. For instance, when using a `:user` resource, the `user_root_path` will be used if it exists; otherwise, the default `root_path` will be used. This means that you need to set the root inside your routes:

```ruby
root to: 'home#index'
```

You can also override `after_sign_in_path_for` and `after_sign_out_path_for` to customize your redirect hooks.

Notice that if your Devise model is called `Member` instead of `User`, for example, then the helpers available are:

```ruby
before_action :authenticate_member!

member_signed_in?

current_member

member_session
```
