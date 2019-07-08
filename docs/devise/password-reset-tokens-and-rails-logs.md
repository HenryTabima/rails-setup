---
id: password-reset-tokens-and-rails-logs
title: Password reset tokens and Rails logs
---

If you enable the [Recoverable](http://rubydoc.info/github/plataformatec/devise/master/Devise/Models/Recoverable) module, note that a stolen password reset token could give an attacker access to your application. Devise takes effort to generate random, secure tokens, and stores only token digests in the database, never plaintext. However the default logging behavior in Rails can cause plaintext tokens to leak into log files:

1. Action Mailer logs the entire contents of all outgoing emails to the DEBUG level. Password reset tokens delivered to users in email will be leaked.
2. Active Job logs all arguments to every enqueued job at the INFO level. If you configure Devise to use `deliver_later` to send password reset emails, password reset tokens will be leaked.

Rails sets the production logger level to DEBUG by default. Consider changing your production logger level to WARN if you wish to prevent tokens from being leaked into your logs. In `config/environments/production.rb`:

```ruby
config.log_level = :warn
```
