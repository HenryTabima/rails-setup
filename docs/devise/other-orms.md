---
id: other-orms
title: Other ORMs
---

Since Devise support both Mongoid and ActiveRecord, we rely on this variable to run specific code for each ORM.
The default value of `DEVISE_ORM` is `active_record`. To run the tests for mongoid, you can pass `mongoid`:
```
DEVISE_ORM=mongoid bin/test

==> Devise.orm = :mongoid
```
When running the tests for Mongoid, you will need to have a MongoDB server (version 2.0 or newer) running on your system.

Please note that the command output will show the variable value being used.