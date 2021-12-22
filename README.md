# Cookie Consent React

* Demo: https://orestbida.com/demo-projects/cookieconsent/

* Git repository: https://github.com/orestbida/cookieconsent/blob/master/Readme.md#api-methods

* NPM: https://www.npmjs.com/package/vanilla-cookieconsent#how-to-configure-languages--cookie-settings


  ### required files
  `cookieconsent.js`  / `cookieconsent.css`


# Installation and Usage

      $ npm i vanilla-cookieconsent
      $ yarn add vanilla-cookieconsent

# Layout options & customization
You can change the color scheme with css variables inside cookieconsent.css. You can also change some basic layout options via the `gui_options` inside the config. object; example:
```js
  cookieconsent.run({
      // ...
      gui_options: {
          consent_modal: {
              layout: 'cloud',               // box/cloud/bar
              position: 'bottom center',     // bottom/middle/top + left/right/center
              transition: 'slide',           // zoom/slide
              swap_buttons: false            // enable to invert buttons
          },
          settings_modal: {
              layout: 'box',                 // box/bar
              position: 'left',           // left/right
              transition: 'slide'            // zoom/slide
          }
      }
      //...
  });
```
      
# API methods
Getting the plugin
```js
var cookieconsent = initCookieConsent();
```

### Method that Available

  * cookieconsent.`run(<config_object>)`
  * cookieconsent.`show(<optional_delay>)`
  * cookieconsent.`hide()`
  * cookieconsent.`showSettings(<optional_delay>)`
  * cookieconsent.`hideSettings()`

Additional methods for an easier management of your scripts and cookie settings


  * cookieconsent.`accept(<accepted_categories>, <optional_rejected_categories>)`
  * cookieconsent.`allowedCategory(<category_name>)`
  * cookieconsent.`validCookie(<cookie_name>)`
  * cookieconsent.`eraseCookies(<cookie_names>, <optional_path>, <optional_domains>)`
  * cookieconsent.`loadScript(<path>, <callback_function>, <optional_custom_attributes>)`
  * cookieconsent.`set(<field>, <object>)`
  * cookieconsent.`get(<field>)`
  * cookieconsent.`getConfig(<field>)`
  * cookieconsent.`getUserPreferences()`


# Available Callback
The following functions have to be defined inside the configuration object passed to the .run() method.
  * `onAccept`
  * `onChange`
  * `onFirstAction`

```js

  onFirstAction: function(user_preferences, cookie){
      // callback triggered only once
  },

  onAccept: function (cookie) {
      // ...
      console.log(cookie)
      console.log(cookie.level) //เช็คว่ากดยอมรับอะไรบ้าง ใน setting => toggle 

  },

  onChange: function (cookie, changed_preferences) {
      // ...
  },


```
  
### All configuration options

The available options (must be passed to the .run() method).
Option | Type | Default | Description
----- | ----- | ----- | ----- |
| `autorun`           	| boolean  	| true    	| If enabled, show the cookie consent as soon as possible (otherwise you need to manually call the `.show()` method)                |
| `delay`             	| number   	| 0       	| Number of `milliseconds` before showing the consent-modal                                                                         |
| `cookie_expiration` 	| number   	| 182     	| Number of days before the cookie expires (182 days = 6 months)                                                                    |
| `cookie_necessary_only_expiration` 	| number   	| -     	| Specify if you want to set a different number of days - before the cookie expires - when the user accepts only the necessary categories                                                |
| `cookie_path` 	    | string   	| "/"     	| Path where the cookie will be set                                                                                                 |
| `cookie_domain` 	    | string   	| location.hostname | Specify your domain (will be grabbed by default) or a subdomain                                                           |
| `cookie_same_site` 	| string   	| "Lax"     | SameSite attribute                                                           |
| `use_rfc_cookie` 	    | boolean   | false     | Enable if you want the value of the cookie to be rfc compliant                                            |
| `theme_css`         	| string   	| -       	| Specify path to the .css file                                             |
| `force_consent`       | boolean   | false     | Enable if you want to block page navigation until user action (check [faq](#faq) for a proper implementation) |
| `revision`            | number  	| 0   	    | Specify this option to enable revisions. [Check below](#how-to-enablemanage-revisions) for a proper usage |
| `current_lang`      	| string   	| -       	| Specify one of the languages you have defined (can also be dynamic): `'en'`, `'de'` ...                                           |
| `auto_language`     	| string  	| null  	| Language auto-detection strategy. Null to disable (default), `"browser"` to get user's browser language or `"document"` to read value from `<html lang="...">` of current page. If language is not defined => use specified `current_lang` |
| `autoclear_cookies` 	| boolean  	| false   	| Enable if you want to automatically delete cookies when user opts-out of a specific category inside cookie settings               |
| `page_scripts` 	    | boolean  	| false   	| Enable if you want to easily `manage existing <script>` tags. Check [manage third party scripts](#manage-third-party-scripts)     |
| `remove_cookie_tables`| boolean  	| false   	| Enable if you want to remove the html cookie tables (but still want to make use of `autoclear_cookies`)                           |
| `hide_from_bots`      | boolean  	| false   	| Enable if you don't want the plugin to run when a bot/crawler/webdriver is detected       |
| `gui_options`         | object  	| -   	    | Customization option which allows to choose layout, position	and transition. Check [layout options & customization](#layout-options--customization) |
| __`onAccept`__      	| function 	| -       	| Method run on: <br>  1. the moment the cookie consent is accepted <br> 2. after each page load (if cookie consent has already been accepted) |
| __`onChange`__      	| function 	| -       	| Method run `whenever preferences are modified` (and only if cookie consent has already been accepted)                             |
| __`onFirstAction`__   | function 	| -       	| Method run only `once` when the user makes the initial choice (accept/reject)                                                     |
| `languages`      	    | object 	| -       	| [Check below](#how-to-configure-languages--cookie-settings) for configuration


