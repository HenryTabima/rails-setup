---
id: installation
title: Installation
---
Devise 4.0 works with Rails 4.1 onwards. Add the following line to your Gemfile:

```ruby
gem 'devise'
```

Then run `bundle install`

Next, you need to run the generator:

```console
$ rails generate devise:install
```

At this point, a number of instructions will appear in the console. Among these instructions, you'll need to set up the default URL options for the Devise mailer in each environment. Here is a possible configuration for `config/environments/development.rb`:

```ruby
config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }
```

The generator will install an initializer which describes ALL of Devise's configuration options. It is *imperative* that you take a look at it. When you are done, you are ready to add Devise to any of your models using the generator.


In the following command you will replace `MODEL` with the class name used for the application’s users (it’s frequently `User` but could also be `Admin`). This will create a model (if one does not exist) and configure it with the default Devise modules. The generator also configures your `config/routes.rb` file to point to the Devise controller.

```console
$ rails generate devise MODEL
```

Next, check the MODEL for any additional configuration options you might want to add, such as confirmable or lockable. If you add an option, be sure to inspect the migration file (created by the generator if your ORM supports them) and uncomment the appropriate section.  For example, if you add the confirmable option in the model, you'll need to uncomment the Confirmable section in the migration.

Then run `rails db:migrate`

You should restart your application after changing Devise's configuration options (this includes stopping spring). Otherwise, you will run into strange errors, for example, users being unable to login and route helpers being undefined.
