---
id: configuring-views
title: Configuring views
---
We built Devise to help you quickly develop an application that uses authentication. However, we don't want to be in your way when you need to customize it.

Since Devise is an engine, all its views are packaged inside the gem. These views will help you get started, but after some time you may want to change them. If this is the case, you just need to invoke the following generator, and it will copy all views to your application:

```console
$ rails generate devise:views
```

If you have more than one Devise model in your application (such as `User` and `Admin`), you will notice that Devise uses the same views for all models. Fortunately, Devise offers an easy way to customize views. All you need to do is set `config.scoped_views = true` inside the `config/initializers/devise.rb` file.

After doing so, you will be able to have views based on the role like `users/sessions/new` and `admins/sessions/new`. If no view is found within the scope, Devise will use the default view at `devise/sessions/new`. You can also use the generator to generate scoped views:

```console
$ rails generate devise:views users
```

If you would like to generate only a few sets of views, like the ones for the `registerable` and `confirmable` module,
you can pass a list of modules to the generator with the `-v` flag.

```console
$ rails generate devise:views -v registrations confirmations
```