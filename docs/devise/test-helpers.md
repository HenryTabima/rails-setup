---
id: test-helpers
title: Test helpers
---

Devise includes some test helpers for controller and integration tests.
In order to use them, you need to include the respective module in your test
cases/specs.

## Controller tests

Controller tests require that you include `Devise::Test::ControllerHelpers` on
your test case or its parent `ActionController::TestCase` superclass.
For Rails 5, include `Devise::Test::IntegrationHelpers` instead, since the superclass
for controller tests has been changed to ActionDispatch::IntegrationTest
(for more details, see the [Integration tests](#integration-tests) section).

```ruby
class PostsControllerTest < ActionController::TestCase
  include Devise::Test::ControllerHelpers
end
```

If you're using RSpec, you can put the following inside a file named
`spec/support/devise.rb` or in your `spec/spec_helper.rb` (or
`spec/rails_helper.rb` if you are using `rspec-rails`):

```ruby
RSpec.configure do |config|
  config.include Devise::Test::ControllerHelpers, type: :controller
  config.include Devise::Test::ControllerHelpers, type: :view
end
```

Just be sure that this inclusion is made *after* the `require 'rspec/rails'` directive.

Now you are ready to use the `sign_in` and `sign_out` methods on your controller
tests:

```ruby
sign_in @user
sign_in @user, scope: :admin
```

If you are testing Devise internal controllers or a controller that inherits
from Devise's, you need to tell Devise which mapping should be used before a
request. This is necessary because Devise gets this information from the router,
but since controller tests do not pass through the router, it needs to be stated
explicitly. For example, if you are testing the user scope, simply use:

```ruby
test 'GET new' do
  # Mimic the router behavior of setting the Devise scope through the env.
  @request.env['devise.mapping'] = Devise.mappings[:user]

  # Use the sign_in helper to sign in a fixture `User` record.
  sign_in users(:alice)

  get :new

  # assert something
end
```

## Integration tests

Integration test helpers are available by including the
`Devise::Test::IntegrationHelpers` module.

```ruby
class PostsTests < ActionDispatch::IntegrationTest
  include Devise::Test::IntegrationHelpers
end
```

Now you can use the following `sign_in` and `sign_out` methods in your integration
tests:

```ruby
sign_in users(:bob)
sign_in users(:bob), scope: :admin

sign_out :user
```

RSpec users can include the `IntegrationHelpers` module on their `:feature` specs.

```ruby
RSpec.configure do |config|
  config.include Devise::Test::IntegrationHelpers, type: :feature
end
```

Unlike controller tests, integration tests do not need to supply the
`devise.mapping` `env` value, as the mapping can be inferred by the routes that
are executed in your tests.

You can read more about testing your Rails 3 - Rails 4 controllers with RSpec in the wiki:

* https://github.com/plataformatec/devise/wiki/How-To:-Test-controllers-with-Rails-(and-RSpec)