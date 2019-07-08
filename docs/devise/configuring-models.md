---
id: configuring-models
title: Configuring Models
---

The Devise method in your models also accepts some options to configure its modules. For example, you can choose the cost of the hashing algorithm with:

```ruby
devise :database_authenticatable, :registerable, :confirmable, :recoverable, stretches: 12
```

Besides `:stretches`, you can define `:pepper`, `:encryptor`, `:confirm_within`, `:remember_for`, `:timeout_in`, `:unlock_in` among other options. For more details, see the initializer file that was created when you invoked the "devise:install" generator described above. This file is usually located at `/config/initializers/devise.rb`.
