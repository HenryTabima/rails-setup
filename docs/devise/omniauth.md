---
id: omniauth
title: OmniAuth
---
> Since version 1.2, Devise supports integration with [OmniAuth](http://github.com/intridea/omniauth). This wiki page will cover the basics to have this integration working using an OAuth provider as example.

> Since version 1.5, Devise supports OmniAuth 1.0 forward which will be the version covered by this tutorial.

Devise comes with OmniAuth support out of the box to authenticate with other providers. To use it, simply specify your OmniAuth configuration in `config/initializers/devise.rb`:

```ruby
config.omniauth :github, 'APP_ID', 'APP_SECRET', scope: 'user,public_repo'
```

## Before you start

Remember that `config.omniauth` adds omniauth provider middleware to your application. This means you should **not** add this provider middleware again in `config/initializers/omniauth.rb` as they'll clash with each other and result in always-failing authentication.

## Facebook example

The first step then is to add an OmniAuth gem to your application. This can be done in our `Gemfile`:

```ruby
gem 'omniauth-facebook'
```

Here we'll use Facebook as an example, but you are free to use whatever and as many OmniAuth gems as you'd like. Generally, the gem name is "omniauth-provider" where provider can be "facebook" or "twitter", for example. For a full list of these providers, please check [OmniAuth's list of strategies](https://github.com/intridea/omniauth/wiki/List-of-Strategies).

Next up, you should add the columns "provider" (string) and "uid" (string) to your User model.

```rails
rails g migration AddOmniauthToUsers provider:string uid:string
rake db:migrate
```

Next, you need to declare the provider in your `config/initializers/devise.rb`:

```ruby
config.omniauth :facebook, "APP_ID", "APP_SECRET"
```

If you are seeing something like _Could not authenticate you from Facebook because “Invalid credentials”_
you may need to add `token_params: { parse: :json }` to your config, i.e.:

```ruby
config.omniauth :facebook, "APP_ID", "APP_SECRET", token_params: { parse: :json }
```

To alter the permissions or scopes requested, check the [omniauth-facebook](https://github.com/mkdynamic/omniauth-facebook) gem's README.

After configuring your strategy, you need to make your model (e.g. `app/models/user.rb`) omniauthable:

```ruby
devise :omniauthable, omniauth_providers: %i[facebook]
```

>**Note**: If you're running a rails server, you'll need to restart it to recognize the change in the `Devise` initializer or adding `:omniauthable` to your `User` model will create an error.

Currently, Devise allows only one model to be omniauthable. If you want to use `OmniAuth` with multiple models, check out [OmniAuth with multiple models](https://github.com/plataformatec/devise/wiki/OmniAuth-with-multiple-models).

After making a model named `User` omniauthable and if `devise_for :users` was already added to your `config/routes.rb`, Devise will create the following url methods:

* user_{provider}_omniauth_authorize_path
* user_{provider}_omniauth_callback_path

Note that Devise does not create `*_url` methods. While you will never use the callback helper above directly, you only need to add the first one to your layouts in order to provide facebook authentication:

```ruby
<%= link_to "Sign in with Facebook", user_facebook_omniauth_authorize_path %>
```

>**Note**: The `{provider}` in the above `*_path` methods matches the symbol of the provider passed to Devise's config block. Please check that `omniauth-*` gem's **README** to know which symbol you should use.

By clicking on the above link, the user will be redirected to `Facebook`. (If this link doesn't exist, try restarting the server.) After inserting their credentials, they will be redirected back to your application's callback method. To implement a callback, the first step is to go back to our `config/routes.rb` file and tell Devise in which controller we will implement Omniauth callbacks:

```ruby
devise_for :users, controllers: { omniauth_callbacks: 'users/omniauth_callbacks' }
```

Now we just add the file `app/controllers/users/omniauth_callbacks_controller.rb`:

```ruby
class Users::OmniauthCallbacksController < Devise::OmniauthCallbacksController
end
```

The callback should be implemented as an action with the same name as the provider. Here is an example action for our facebook provider that we could add to our controller:

```ruby
class Users::OmniauthCallbacksController < Devise::OmniauthCallbacksController
  def facebook
    # You need to implement the method below in your model (e.g. app/models/user.rb)
    @user = User.from_omniauth(request.env["omniauth.auth"])

    if @user.persisted?
      sign_in_and_redirect @user, event: :authentication #this will throw if @user is not activated
      set_flash_message(:notice, :success, kind: "Facebook") if is_navigational_format?
    else
      session["devise.facebook_data"] = request.env["omniauth.auth"]
      redirect_to new_user_registration_url
    end
  end

  def failure
    redirect_to root_path
  end
end
```

This action has a few aspects worth describing:

1. All information retrieved from Facebook by OmniAuth is available as a hash at `request.env["omniauth.auth"]`. Check the [OmniAuth docs](https://github.com/intridea/omniauth/wiki/Auth-Hash-Schema) and each [omniauth-facebook](https://github.com/mkdynamic/omniauth-facebook#auth-hash) gem's README to know which information is being returned.

2. When a valid user is found, they can be signed in with one of two Devise methods: `sign_in` or `sign_in_and_redirect`. Passing `:event => :authentication` is optional. You should only do so if you wish to use [Warden callbacks](http://stackoverflow.com/a/13389324/1160916).

3. A flash message can also be set using one of Devise's default messages, but that is up to you.

4. In case the user is not persisted, we store the OmniAuth data in the session. Notice we store this data using "devise." as key namespace. This is useful because Devise removes all the data starting with "devise." from the session whenever a user signs in, so we get automatic session clean up. At the end, we redirect the user back to our registration form.

After the controller is defined, we need to implement the `from_omniauth` method in our model (e.g. `app/models/user.rb`):

```ruby
def self.from_omniauth(auth)
  where(provider: auth.provider, uid: auth.uid).first_or_create do |user|
    user.email = auth.info.email
    user.password = Devise.friendly_token[0, 20]
    user.name = auth.info.name   # assuming the user model has a name
    user.image = auth.info.image # assuming the user model has an image
    # If you are using confirmable and the provider(s) you use validate emails,
    # uncomment the line below to skip the confirmation emails.
    # user.skip_confirmation!
  end
end
```

This method tries to find an existing user by the `provider` and `uid` fields. If no user is found, a new one is created with a random password and some extra information.
Note that the [`first_or_create` method](http://apidock.com/rails/v3.2.1/ActiveRecord/Relation/first_or_create) automatically sets the `provider` and `uid` fields when creating a new user. The [`first_or_create!` method](http://apidock.com/rails/v3.2.1/ActiveRecord/Relation/first_or_create!) operates similarly, except that it will raise an Exception if the user record fails validation.

Notice that Devise's `RegistrationsController` by default calls `User.new_with_session` before building a resource. This means that, if we need to copy data from session whenever a user is initialized before sign up, we just need to implement `new_with_session` in our model. Here is an example that copies the facebook email if available:

```ruby
class User < ApplicationRecord
  def self.new_with_session(params, session)
    super.tap do |user|
      if data = session["devise.facebook_data"] && session["devise.facebook_data"]["extra"]["raw_info"]
        user.email = data["email"] if user.email.blank?
      end
    end
  end
end
```

Finally, if you want to allow your users to cancel sign up with Facebook, you can redirect them to `cancel_user_registration_path`. This will remove all session data starting with `devise.` and the `new_with_session` hook above will no longer be called.

### Logout links


```ruby
# config/routes.rb
devise_scope :user do
  delete 'sign_out', :to => 'devise/sessions#destroy', :as => :destroy_user_session
end
```

And that is all you need! After you get your integration working, it's time to write some integration tests:

[https://github.com/intridea/omniauth/wiki/Integration-Testing](https://github.com/intridea/omniauth/wiki/Integration-Testing)

## Using OmniAuth without other authentications

If you are using **ONLY** omniauth authentication, you need to define a route named `new_user_session` (if not defined, root will be used). Below is an example of such routes (you don't need to include it if you are also using database or other authentication with omniauth):

```ruby
devise_for :users, :controllers => { :omniauth_callbacks => "users/omniauth_callbacks" }

devise_scope :user do
  get 'sign_in', :to => 'devise/sessions#new', :as => :new_user_session
  get 'sign_out', :to => 'devise/sessions#destroy', :as => :destroy_user_session
end
```

In the example above, the sessions controller doesn't need to do anything special. For example, showing a link to the provider authentication will suffice.

> **Note**: If your Devise configuration specifies `sign_out_via = :delete`, you may need to adjust your sign_out route to match an incoming DELETE request instead.

Also, if you are not using `:database_authenticatable` you have to define the helper method `new_session_path(scope)` so it can correctly redirect in case of failure:

```ruby
class ApplicationController < ActionController::Base
# ...
  def new_session_path(scope)
    new_user_session_path
  end
end
```

## Troubleshooting

### User didn't allow email permissions

In the new Facebook login dialog the user can decline to provide email address.
Devise usually requires email to register. A quick and dirty solution to this problem is to re-request the email if it wasn't found:

```ruby
class Users::OmniauthCallbacksController < Devise::OmniauthCallbacksController
  def facebook
    if request.env["omniauth.auth"].info.email.blank?
      redirect_to "/users/auth/facebook?auth_type=rerequest&scope=email"
      return # be sure to include an return if there is code after this otherwise it will be executed
    end
  end
end
```

### Facebook returning nulled email

Since July 8th 2015 Facebook changed to api v2.4, you need to add extra `info_fields` to get email field.
```ruby
config.omniauth :facebook, "APP_ID", "APP_SECRET", scope: 'email', info_fields: 'email,name'
```
[found solution from here by @techmonster](https://www.digitalocean.com/community/tutorials/how-to-configure-devise-and-omniauth-for-your-rails-application)

If this solution doesn't work for you. Please, try to use fields instead of info_fields.

### Extra config

Facebook OAuth gem uses the API version `V2.6` by default.
This might not work for you, as your app might be configured to use a different version of GraphAPI.
So you need to make sure your web-app is making the correct call.
You need to add extra option `client_options`. See an example:

```ruby
config.omniauth :facebook, ENV['FB_APP_ID'], ENV['FB_APP_SECRET'],
                scope: 'public_profile,email',
                info_fields: 'email,first_name,last_name,gender,birthday,location,picture',
                client_options: {
                    site: 'https://graph.facebook.com/v2.11',
                    authorize_url: "https://www.facebook.com/v2.11/dialog/oauth"
                }
```

### OpenSSL

If you run into an OpenSSL error like this:

```ruby
OpenSSL::SSL::SSLError (SSL_connect returned=1 errno=0 state=SSLv3 read server certificate B: certificate verify failed):
```

Then you need to explicitly tell OmniAuth where to locate your CA certificate file.
Either use the [certified gem](https://github.com/stevegraham/certified) or this method (depending on the OS you are running on):

```ruby
config.omniauth :facebook, "APP_ID", "APP_SECRET",
  client_options: { ssl: { ca_path: '/etc/ssl/certs' } }
```

On Heroku, the CA file is located at `/usr/lib/ssl/certs/ca-certificates.crt`

On Engine Yard Cloud servers, the CA file is located at `/etc/ssl/certs/ca-certificates.crt`.

These certificates can be set using the `:ca_file` key:

```ruby
config.omniauth :facebook, "APP_ID", "APP_SECRET",
  client_options: { ssl: { ca_file: '/usr/lib/ssl/certs/ca-certificates.crt' } }
```

If you are using a strategy that uses the OAuth gem eg [omniauth-oauth](https://github.com/intridea/omniauth-oauth) then specify the certificate file this way:

```ruby
config.omniauth :facebook, "APP_ID", "APP_SECRET",
  client_options: { ca_file: '/usr/lib/ssl/certs/ca-certificates.crt' }
```

On macOS, for development only, it may be easiest just to disable certificate verification because the certificates are stored in the keychain, not the file system:

```ruby
require "omniauth-facebook"
config.omniauth :facebook, "APP_ID", "APP_SECRET", client_options: { ssl: { verify: !Rails.env.development? } }
```

A deeper discussion of this error can be found here: https://github.com/intridea/omniauth/issues/260

### Cannot load strategy class

If for some reason Devise cannot load your strategy class, you can set it explicitly with the `:strategy_class` option:

```ruby
config.omniauth :facebook, "APP_ID", "APP_SECRET", :strategy_class => OmniAuth::Strategies::Facebook
```
