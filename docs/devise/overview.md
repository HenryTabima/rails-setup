---
id: overview
title: Overview
---
![Devise Logo](https://raw.github.com/plataformatec/devise/master/devise.png)

By [Plataformatec](http://plataformatec.com.br/).

Devise is a flexible authentication solution for Rails based on Warden. It:

* Is Rack based;
* Is a complete MVC solution based on Rails engines;
* Allows you to have multiple models signed in at the same time;
* Is based on a modularity concept: use only what you really need.

## Modules

It's composed of 10 modules:

* [Database Authenticatable](http://www.rubydoc.info/github/plataformatec/devise/master/Devise/Models/DatabaseAuthenticatable): hashes and stores a password in the database to validate the authenticity of a user while signing in. The authentication can be done both through POST requests or HTTP Basic Authentication.
* [Omniauthable](http://www.rubydoc.info/github/plataformatec/devise/master/Devise/Models/Omniauthable): adds OmniAuth (https://github.com/omniauth/omniauth) support.
* [Confirmable](http://www.rubydoc.info/github/plataformatec/devise/master/Devise/Models/Confirmable): sends emails with confirmation instructions and verifies whether an account is already confirmed during sign in.
* [Recoverable](http://www.rubydoc.info/github/plataformatec/devise/master/Devise/Models/Recoverable): resets the user password and sends reset instructions.
* [Registerable](http://www.rubydoc.info/github/plataformatec/devise/master/Devise/Models/Registerable): handles signing up users through a registration process, also allowing them to edit and destroy their account.
* [Rememberable](http://www.rubydoc.info/github/plataformatec/devise/master/Devise/Models/Rememberable): manages generating and clearing a token for remembering the user from a saved cookie.
* [Trackable](http://www.rubydoc.info/github/plataformatec/devise/master/Devise/Models/Trackable): tracks sign in count, timestamps and IP address.
* [Timeoutable](http://www.rubydoc.info/github/plataformatec/devise/master/Devise/Models/Timeoutable): expires sessions that have not been active in a specified period of time.
* [Validatable](http://www.rubydoc.info/github/plataformatec/devise/master/Devise/Models/Validatable): provides validations of email and password. It's optional and can be customized, so you're able to define your own validations.
* [Lockable](http://www.rubydoc.info/github/plataformatec/devise/master/Devise/Models/Lockable): locks an account after a specified number of failed sign-in attempts. Can unlock via email or after a specified time period.

## RDocs (API)

You can view the Devise documentation in RDoc format here:

http://rubydoc.info/github/plataformatec/devise/master/frames

If you need to use Devise with previous versions of Rails, you can always run "gem server" from the command line after you install the gem to access the old documentation.


## StackOverflow and Mailing List

If you have any questions, comments, or concerns, please use StackOverflow instead of the GitHub issue tracker:

http://stackoverflow.com/questions/tagged/devise

The deprecated mailing list can still be read on

https://groups.google.com/group/plataformatec-devise


## Running tests
Devise uses [Mini Test](https://github.com/seattlerb/minitest) as test framework.

* Running all tests:
```bash
bin/test
```

* Running tests for an specific file:
```bash
bin/test test/models/trackable_test.rb
```

* Running a specific test given a regex:
```bash
bin/test test/models/trackable_test.rb:16
```

## Contributors

We have a long list of valued contributors. Check them all at:

https://github.com/plataformatec/devise/graphs/contributors

## License

MIT License. Copyright 2009-2018 Plataformatec. http://plataformatec.com.br

You are not granted rights or licenses to the trademarks of Plataformatec, including without limitation the Devise name or logo.