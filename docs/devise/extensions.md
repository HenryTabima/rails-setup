---
id: extensions
title: List of 3rd party Devise extensions.
sidebar_label: Extensions
---

## ORM Support

*mm-devise* - "Devise - MongoMapper":http://github.com/kristianmandrup/mm-devise

*dm-devise* - "Devise - DataMapper":http://github.com/jm81/dm-devise

*devise-couch* -  "Devise - Couch DB":http://github.com/shenoudab/devise_couch

*devise-ripple* - "Devise - Riak":http://github.com/frank06/devise-ripple

*cequel-devise* - "Devise - Cassandra":https://github.com/cequel/cequel-devise

## Encryption Support

*devise-encryptable* - adds support of other authentication mechanisms besides the built-in Bcrypt (the default).
"https://github.com/plataformatec/devise-encryptable":https://github.com/plataformatec/devise-encryptable

*devise_aes_encryptable* - AES-256 Reversible Encryption
"http://github.com/chicks/devise_aes_encryptable":http://github.com/chicks/devise_aes_encryptable

*devise-argon2* - Support for Argon2i
"https://github.com/erdostom/devise-argon2":https://github.com/erdostom/devise-argon2

## Mailing List Support

*devise_campaignable* - Have your users automatically added to a mail campaign tool of your choice. Currently supports MailChimp but easy adaptation for CampaignMonitor. "https://github.com/SirRawlins/devise_campaignable":https://github.com/SirRawlins/devise_campaignable

*devise_mailchimp* - MailChimp integration for Devise making it effortless for users to join mailing lists when they register their account.
"http://jcnnghm.github.com/devise_mailchimp/":http://jcnnghm.github.com/devise_mailchimp/

h3. Miscellaneous

*cantango* - Integrates Devise, Roles and CanCan with Permits for a Rails 3 app
"http://github.com/kristianmandrup/cantango":http://github.com/kristianmandrup/cantango
(Replaces *cream*, "http://github.com/kristianmandrup/cream":http://github.com/kristianmandrup/cream)

*invitable* - Adds support for send account invitations by email.
"http://github.com/scambra/devise_invitable":http://github.com/scambra/devise_invitable

*devise_traceable* - Tracing Devise Model (Model Stamp login and logout)
"http://github.com/shenoudab/devise_traceable":http://github.com/shenoudab/devise_traceable

*devise_lastseenable* - Just adds a last_seen datetime that's updated whenever authenticate! is called.
"https://github.com/ctide/devise_lastseenable":https://github.com/ctide/devise_lastseenable

*devise_security* - Add "enterprise" functionality (strong passwords, password expire..., new: captcha support)
"https://github.com/devise-security/devise-security":https://github.com/devise-security/devise-security

*devise-basecamper* - Add basecamp-style subdomain scoped authentication
"https://github.com/digitalopera/devise-basecamper":https://github.com/digitalopera/devise-basecamper

*devise-two-factor* - Barebones two-factor authentication support
"https://github.com/tinfoil/devise-two-factor":https://github.com/tinfoil/devise-two-factor

*two_factor_authentication* - Add two factor authentication, like Gmail
"https://github.com/Houdini/two_factor_authentication":https://github.com/Houdini/two_factor_authentication

*devise_account_expireable* - Expire a user account at a specific date / time.
"https://github.com/j-mcnally/devise_account_expireable":https://github.com/j-mcnally/devise_account_expireable

*devise_uid* - Add UID support to Devise. A lot of times, we want a unique ID representing the user model instead of its incremental ID in the database, for example, in API instead of exposing the primary key, we use a random generated unique string to indentify this user.
"https://github.com/jingweno/devise_uid":https://github.com/jingweno/devise_uid

*devise_session_expirable* - Devise timeoutable's paranoid cousin. Enforces time-limited sessions by rejecting sessions which are not timestamped.
"https://github.com/teleological/devise_session_expirable":https://github.com/teleological/devise_session_expirable

*devise_zxcvbn* - Reject weak passwords using zxcvbn.
"https://github.com/bitzesty/devise_zxcvbn":https://github.com/bitzesty/devise_zxcvbn

*devise_invalidatable* - Invalidate sessions from the server-side.
"https://github.com/madkins/devise_invalidatable":https://github.com/madkins/devise_invalidatable

*any_login* - easy login with any user to make your development life easier.
"https://github.com/igorkasyanchuk/any_login":https://github.com/igorkasyanchuk/any_login

*devise-verifiable* - Adds a second step to Devise's signup process. Useful if you want to collect extra information or verify user's identity through a 3rd-party service. "github.com/Rodrigora/devise-verifiable":https://github.com/Rodrigora/devise-verifiable

*honeybadger* - When used together, exceptions reported to honeybadger will automatically be associated with the current Devise user.
"https://github.com/honeybadger-io/honeybadger-ruby":https://github.com/honeybadger-io/honeybadger-ruby

*devise-uncommon_password* - Prevents a user from using a password in the list of the 100 most common passwords.
"https://github.com/HCLarsen/devise-uncommon_password":https://github.com/HCLarsen/devise-uncommon_password

*devise-pwned_password* - checks user passwords against the "PwnedPasswords":https://haveibeenpwned.com/Passwords dataset.
"https://github.com/michaelbanfield/devise-pwned_password":https://github.com/michaelbanfield/devise-pwned_password

*devise_date_restrictable* - restrict a user’s account by date range (valid from/until/between).
"https://github.com/jonpearse/devise_date_restrictable":https://github.com/jonpearse/devise_date_restrictable

h3. External authentication integration

*devise-browserid* - Adds support for Mozilla Persona / BrowserID authentication.
"https://github.com/ringe/devise-browserid/":https://github.com/ringe/devise-browserid/

*facebook_connectable* - Adds support for Facebook Connect authentication, and optionally fetching user info from Facebook in the same step.
"http://github.com/grimen/devise_facebook_connectable":http://github.com/grimen/devise_facebook_connectable

*oauth2_authenticatable* - Adds support for OAuth2 (Facebook Graph) authentication.
"http://github.com/bhbryant/devise_oauth2_authenticatable":http://github.com/bhbryant/devise_oauth2_authenticatable

*oauth2_providable* - Adds an OAuth2 authentication layer to protect API resources.
"https://github.com/socialcast/devise_oauth2_providable":https://github.com/socialcast/devise_oauth2_providable

*devise-twitter* - Adds Sign in via Twitter and Connect your account to Twitter functionality
"http://github.com/MSch/devise-twitter":http://github.com/MSch/devise-twitter

*imapable* - Adds support for authentication via IMAP, a great solution for internal application where no LDAP server exists.
"http://github.com/joshk/devise_imapable":http://github.com/joshk/devise_imapable

*ldap_authenticatable* - Adds support for LDAP authentication via simple bind.
"http://github.com/cschiewek/devise_ldap_authenticatable":http://github.com/cschiewek/devise_ldap_authenticatable

*rpx_connectable* - Adds support for "RPX":http://www.rpxnow.com authentication. "RPX":http://www.rpxnow.com provides free and paid services to handle many authentication providers (facebook, twitter, OpenID...) using a single API.
"http://github.com/slainer68/devise_rpx_connectable":http://github.com/slainer68/devise_rpx_connectable

*cas_authenticatable* - Adds support for single sign-on via "CAS":http://www.jasig.org/cas and CAS-implementing servers.
"http://github.com/nbudin/devise_cas_authenticatable":http://github.com/nbudin/devise_cas_authenticatable

*openid_authenticatable* - Adds support for "OpenID":http://openid.net authentication.
"http://github.com/nbudin/devise_openid_authenticatable":http://github.com/nbudin/devise_openid_authenticatable

*devise_paypal* - Adds support for "Paypal":http://www.paypal.com authentication
"http://github.com/dwilkie/devise_paypal":http://github.com/dwilkie/devise_paypal

*devise_google_authenticator* - Adds support for "Google's Authenticator":http://code.google.com/p/google-authenticator/
"http://github.com/AsteriskLabs/devise_google_authenticator":http://github.com/AsteriskLabs/devise_google_authenticator

*devise_shibboleth_authenticatable* - Adds support for "Shibboleth":http://shibboleth.net
"https://github.com/jgeorge300/devise_shibboleth_authenticatable":https://github.com/jgeorge300/devise_shibboleth_authenticatable

*devise-radius-authenticatable* - Adds support for authenticating against radius servers
"https://github.com/cbascom/devise-radius-authenticatable":https://github.com/cbascom/devise-radius-authenticatable

*devise-jwt* - JWT token authentication with devise
"https://github.com/waiting-for-dev/devise-jwt":https://github.com/waiting-for-dev/devise-jwt