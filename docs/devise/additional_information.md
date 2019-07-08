---
id: additional-information
title: Additional information
---

## Heroku

Using Devise on Heroku with Ruby on Rails 3.2 requires setting:

```ruby
config.assets.initialize_on_precompile = false
```

Read more about the potential issues at http://guides.rubyonrails.org/asset_pipeline.html

## Warden

Devise is based on Warden, which is a general Rack authentication framework created by Daniel Neighman. We encourage you to read more about Warden here:

https://github.com/hassox/warden

## DEVISE_ORM


## BUNDLE_GEMFILE
We can use this variable to tell bundler what Gemfile it should use (instead of the one in the current directory).
Inside the [gemfiles](https://github.com/plataformatec/devise/tree/master/gemfiles) directory, we have one for each version of Rails we support. When you send us a pull request, it may happen that the test suite breaks on Travis using some of them. If that's the case, you can simulate the same environment using the `BUNDLE_GEMFILE` variable.
For example, if the tests broke using Ruby 2.4.2 and Rails 4.1, you can do the following:
```bash
rbenv shell 2.4.2 # or rvm use 2.4.2
BUNDLE_GEMFILE=gemfiles/Gemfile.rails-4.1-stable bundle install
BUNDLE_GEMFILE=gemfiles/Gemfile.rails-4.1-stable bin/test
```

You can also combine both of them if the tests broke for Mongoid:
```bash
BUNDLE_GEMFILE=gemfiles/Gemfile.rails-4.1-stable bundle install
BUNDLE_GEMFILE=gemfiles/Gemfile.rails-4.1-stable DEVISE_ORM=mongoid bin/test
```
