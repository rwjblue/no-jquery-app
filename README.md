# no-jquery-app

This app is an example of how to setup an ember-cli app to work without jQuery being included in `vendor.js`.

## Steps

First, install [ember-native-dom-event-dispatcher](https://github.com/rwjblue/ember-native-dom-event-dispatcher/)
(as done in [4b0bfec](https://github.com/rwjblue/no-jquery-app/commit/a4b0bfec32618a98322f225d613fb243489aecf6)).

```
ember install ember-native-dom-event-dispatcher
```


Next, add the following snippet to your `ember-cli-build.js` (as done in [34c40fc](https://github.com/rwjblue/no-jquery-app/commit/34c40fc2cfc5e2ce0c39e5e906448c46af699d26)):

```diff
--- a/ember-cli-build.js
+++ b/ember-cli-build.js
@@ -4,6 +4,9 @@ const EmberApp = require('ember-cli/lib/broccoli/ember-app');
 module.exports = function(defaults) {
   var app = new EmberApp(defaults, {
     // Add options here
+    vendorFiles: {
+      'jquery.js': null
+    }
   });

   // Use `app.import` to add additional libraries to the generated
```

Thats it!

## Caveats

* A number of existing addons may rely on usage of `jQuery`.
* Acceptance test helpers within Ember rely on `jQuery` usage. This can be mitigated by using `ember-native-dom-helpers` instead of the native `click` / `fillIn` / etc helpers.
* More? Open an issue...
