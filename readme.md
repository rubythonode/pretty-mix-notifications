# Pretty Laravel Mix Notifications

Take 2 seconds to make your laravel-mix notifications pretty.

![success](https://user-images.githubusercontent.com/20874606/40872928-cbd4a51e-665f-11e8-992d-e496f0e5ff1d.png)
![failure](https://user-images.githubusercontent.com/20874606/40872942-e648f9f4-665f-11e8-8966-486ef6ef4e46.png)

## Installation

  1. `npm install pretty-mix-notifications --save-dev` or `yarn add pretty-mix-notifications --dev`
  2. Require the package to your webpack.mix.js file `let Notifications = require('pretty-mix-notifications');`
  3. Extend mix, and pass it the package. `mix.extend('prettyNotifications', new Notifications);`
  4. Call the prettyNotifications.
  
  Here is a full example of a **webpack.mix.js** file that uses this package:
  
  ```javascript
     let mix = require('laravel-mix');
     let Notifications = require('pretty-mix-notifications');
     
     mix.extend('prettyNotifications', new Notifications);
     
     /*
      |--------------------------------------------------------------------------
      | Mix Asset Management
      |--------------------------------------------------------------------------
      |
      | Mix provides a clean, fluent API for defining some Webpack build steps
      | for your Laravel application. By default, we are compiling the Sass
      | file for the application as well as bundling up all the JS files.
      |
      */
     
     mix.js('resources/assets/js/app.js', 'public/js')
        .sass('resources/assets/sass/app.scss', 'public/css')
         .prettyNotifications();
  ```
  
## Override the default config

If you want to override the default configuration you can pass an object with your config to the prettyNotifications function.

Below we override the default **successIcon** and the default **title**.

 ```javascript
     mix.js('resources/assets/js/app.js', 'public/js')
        .sass('resources/assets/sass/app.scss', 'public/css')
         .prettyNotifications(
             {
                 title: "Pretty Mix Notifications",
                 
                 successIcon: path.resolve("./success.png"), 
             }
         );
  ```

## Config Options
 
 Here is the full list of the supported configuration. You can also pass any valid [node-notifier](https://github.com/mikaelbr/node-notifier) option, that may not be listed here. Just keep in mind, that not every option of node-notifier works in the **Windows platform**.
 
 #### title
 The notification title. Defaults to **_Laravel-Mix build_**.
 
 #### logo
 The absolute path to the project logo to be displayed as a content image in the notification. Optional.
 
 #### successSound
 The sound to play for success notifications. Defaults to the value of the **submarine** for mac OS and **Notification.Default** for windows. Set to false to play no sound for success notifications.
 * In Mac OS successSound can be one of these: Basso, Blow, Bottle, Frog, Funk, Glass, Hero, Morse, Ping, Pop, Purr, Sosumi, Submarine, Tink. If sound is simply true, Bottle is used.
 * In Linux OS there are no sounds.
 * In windows you can choose any valid option described [here](http://msdn.microsoft.com/en-us/library/windows/apps/hh761492.aspx). e.g. `successSound: 'Notification.Mail'` 
 
 #### warningSound
 The sound to play for warning notifications. Defaults to the value of the **submarine** for mac OS and **Notification.Default** for windows. Set to false to play no sound for success notifications.
  * In Mac OS warningSound can be one of these: Basso, Blow, Bottle, Frog, Funk, Glass, Hero, Morse, Ping, Pop, Purr, Sosumi, Submarine, Tink. If sound is simply true, Bottle is used.
  * In Linux OS there are no sounds.
  * In windows you can choose any valid option described [here](http://msdn.microsoft.com/en-us/library/windows/apps/hh761492.aspx). e.g. `warningSound: 'Notification.Mail'`
 
 #### failureSound
 The sound to play for failure notifications. Defaults to the value of the **submarine** for mac OS and **Notification.Default** for windows. Set to false to play no sound for success notifications.
  * In Mac OS failureSound can be one of these: Basso, Blow, Bottle, Frog, Funk, Glass, Hero, Morse, Ping, Pop, Purr, Sosumi, Submarine, Tink. If sound is simply true, Bottle is used.
  * In Linux OS there are no sounds.
  * In windows you can choose any valid option described [here](http://msdn.microsoft.com/en-us/library/windows/apps/hh761492.aspx). e.g. `failureSound: 'Notification.Mail'`
 
 #### suppressSuccess
 Defines when success notifications are shown. Can be one of the following values:
 *  false     - Show success notification for each successful compilation (default).
 *  true      - Only show success notification for initial successful compilation and after failed compilations.
 *  "always"  - Never show the success notifications.
 *  "initial" - Same as true, but suppresses the initial success notification.
 
 #### suppressWarning
 True to suppress the warning notifications, otherwise false (default).
 
 #### suppressCompileStart
 True to suppress the compilation started notifications (default), otherwise false.
 
 #### activateTerminalOnError
 True to activate (focus) the terminal window when a compilation error occurs. Note that this only works on Mac OSX (for now). Defaults to **_false_**. Regardless of the value of this config option, the terminal window can always be brought to the front by clicking on the notification.
 
 #### successIcon
 The absolute path to the icon to be displayed for success notifications. Defaults to the included **_./icons/success.png_**.
 
 #### warningIcon
 The absolute path to the icon to be displayed for warning notifications. Defaults to the included **_./icons/warning.png_**.
 
 #### failureIcon
 The absolute path to the icon to be displayed for failure notifications. Defaults to the included **_./icons/failure.png_**.
 
 #### compileIcon
 The absolute path to the icon to be displayed for compilation started notifications. Defaults to the included **_./icons/compile.png_**.
 
 #### messageFormatter
 A function which returns a formatted notification message. The function is passed two parameters:
 * {Object} error/warning - The raw error or warning object.
 * {String} filepath - The path to the file containing the error/warning (if available).
 
 This function must return a String.
 The default messageFormatter will display the filename which contains the error/warning followed by the
 error/warning message.
 Note that the message will always be limited to 256 characters.
 
 #### onClick
 A function to be called when the notification is clicked. By default it activates the Terminal application. (Does not work on windows)
 
 The function's signature
 ```javascript
{
    // other options
    onClick: function(notifierObject, options){}
}
```
 #### onTimeout
 A function to be called when the notification closes. By default it does not do anything.
 
  The function's signature
  ```javascript
 //Configuration options
 {
     // other options
     onTimeout: function(notifierObject, options){}
 }
 ```
 
 ## Contributing
 
 Thank you for considering contributing to the Pretty Mix Notifications.
 
 ## License
 
 Pretty Mix Notifications is open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT).