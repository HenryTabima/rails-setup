---
id: bug-reports
title: Bug reports
---
If you were linked to this page from Github Issues Tracker or Mailing List, don't worry! We still love you and want your feedback, but you may have left some important information out of your report. Please read below.

First off: if you have questions about Devise, please search the Wiki and Google Group to see if your questions have already been answered. If not, please post your questions to the Google Group. *Do not use the GitHub Issues tracker for questions*

1) Before submitting a bug report:

* Ensure you are using latest devise version. If you are using Devise from git repository with bundler, be sure to run `bundle update`. Maybe your error was already fixed.
* Search the existing GitHub Issues to make sure your issue hasn't already been reported. If not, proceed.
* If you found a security bug, do *NOT* use the GitHub Issue tracker. Please send an email to opensource@plataformatec.com.br.

2) When submitting a bug report:

* Include Ruby, Warden, Devise, OrmAdapter (if using Devise 1.2 forward) and Rails versions in the report;
* Include oauth2 and faraday gem versions if using OAuth;
* Include error class, message and backtrace if you are getting an error;

3) The information above can help us spot an obvious bug, however most bugs may require you to investigate deeper. In such cases:

* Please try to reproduce the bug in devise test suite. Devise test suite is a Rails application as any other (check test/rails_app in the repository) making it easy to reproduce bugs;
* Or try to isolate the bug in a smaller application and push it to github;

Remember that this is an open-source project, and the contributions of volunteers have made it possible. Please be polite and provide as much information as possible so that we can help you!

4) Our Issues Tracker is available here:

http://github.com/plataformatec/devise/issues
