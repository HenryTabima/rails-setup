---
id: rails-api-mode
title: Rails API mode
---

Rails 5+ has a built-in [API Mode](https://edgeguides.rubyonrails.org/api_app.html) which optimizes Rails for use as an API (only). One of the side effects is that it changes the order of the middleware stack, and this can cause problems for `Devise::Test::IntegrationHelpers`. This problem usually surfaces as an ```undefined method `[]=' for nil:NilClass``` error when using integration test helpers, such as `#sign_in`. The solution is simply to reorder the middlewares by adding the following to test.rb:

```ruby
Rails.application.config.middleware.insert_before Warden::Manager, ActionDispatch::Cookies
Rails.application.config.middleware.insert_before Warden::Manager, ActionDispatch::Session::CookieStore
```

For a deeper understanding of this, review [this issue](https://github.com/plataformatec/devise/issues/4696).