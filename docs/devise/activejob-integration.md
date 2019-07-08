---
id: activejob-integration
title: ActiveJob integration
---

If you are using Rails 4.2 and ActiveJob to deliver ActionMailer messages in the
background through a queuing back-end, you can send Devise emails through your
existing queue by overriding the `send_devise_notification` method in your model.

```ruby
def send_devise_notification(notification, *args)
  devise_mailer.send(notification, self, *args).deliver_later
end
```