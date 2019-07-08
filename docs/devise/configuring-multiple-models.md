---
id: configuring-multiple-models
title: Configuring multiple models
---

Devise allows you to set up as many Devise models as you want. If you want to have an Admin model with just authentication and timeout features, in addition to the User model above, just run:

```ruby
# Create a migration with the required fields
create_table :admins do |t|
  t.string :email
  t.string :encrypted_password
  t.timestamps null: false
end

# Inside your Admin model
devise :database_authenticatable, :timeoutable

# Inside your routes
devise_for :admins

# Inside your protected controller
before_action :authenticate_admin!

# Inside your controllers and views
admin_signed_in?
current_admin
admin_session
```

Alternatively, you can simply run the Devise generator.

Keep in mind that those models will have completely different routes. They **do not** and **cannot** share the same controller for sign in, sign out and so on. In case you want to have different roles sharing the same actions, we recommend that you use a role-based approach, by either providing a role column or using a dedicated gem for authorization.