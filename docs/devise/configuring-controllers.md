---
id: configuring-controllers
title: Configuring controllers
---

If the customization at the views level is not enough, you can customize each controller by following these steps:

1. Create your custom controllers using the generator which requires a scope:

    ```console
    $ rails generate devise:controllers [scope]
    ```

    If you specify `users` as the scope, controllers will be created in `app/controllers/users/`.
    And the sessions controller will look like this:

    ```ruby
    class Users::SessionsController < Devise::SessionsController
      # GET /resource/sign_in
      # def new
      #   super
      # end
      ...
    end
    ```
    (Use the -c flag to specify a controller, for example: `rails generate devise:controllers users -c=sessions`)

2. Tell the router to use this controller:

    ```ruby
    devise_for :users, controllers: { sessions: 'users/sessions' }
    ```

3. Copy the views from `devise/sessions` to `users/sessions`. Since the controller was changed, it won't use the default views located in `devise/sessions`.

4. Finally, change or extend the desired controller actions.

    You can completely override a controller action:

    ```ruby
    class Users::SessionsController < Devise::SessionsController
      def create
        # custom sign-in code
      end
    end
    ```

    Or you can simply add new behaviour to it:

    ```ruby
    class Users::SessionsController < Devise::SessionsController
      def create
        super do |resource|
          BackgroundWorker.trigger(resource)
        end
      end
    end
    ```

    This is useful for triggering background jobs or logging events during certain actions.

Remember that Devise uses flash messages to let users know if sign in was successful or unsuccessful. Devise expects your application to call `flash[:notice]` and `flash[:alert]` as appropriate. Do not print the entire flash hash, print only specific keys. In some circumstances, Devise adds a `:timedout` key to the flash hash, which is not meant for display. Remove this key from the hash if you intend to print the entire hash.
