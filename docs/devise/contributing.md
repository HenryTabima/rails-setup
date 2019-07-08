---
id: contributing
title: Contributing
---
We hope that you will consider contributing to Devise. You can contribute in many ways. For example, you might:

* add documentation and "how-to" articles to the README or Wiki.
* help people with the questions they ask on the Google Group.
* create an extension that provides additional functionality above and beyond Devise itself.
* improve the existing example applications to demonstrate features in Devise.
* improve and/or add new I18n translations
* hack on Devise itself by fixing bugs you've found in the GitHub Issue tracker or adding new features to Devise.

When contributing to Devise, we ask that you:

* let us know what you plan in the GitHub Issue tracker so we can provide feedback.
* provide tests and documentation whenever possible. It is very unlikely that we will accept new features or functionality into Devise without the proper testing and documentation. When fixing a bug, provide a failing test case that your patch solves.
* open a GitHub Pull Request with your patches and we will review your contribution and respond as quickly as possible. Keep in mind that this is an open source project, and it may take us some time to get back to you. Your patience is very much appreciated.

We have a long list of valued contributors. Check them all at:

http://github.com/plataformatec/devise/contributors

= Testing

You can run the entire test suite with the default rake task:

```
rake
```

To run a single test, specify the file in the `TEST` environment variable:

```
rake test TEST=test/controllers/passwords_controller_test.rb
```