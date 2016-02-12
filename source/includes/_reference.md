# Reference


## window.ramenSettings

All the options you can set on ramenSettings, the same object
you can pass to `Ramen.Api.update(config)` for subsequent updates.

```javascript
window.ramenSettings = {
  /*
   * Core Options
   */
  // Your Organization ID
  // Required
  organization_id: "",

  // The currently logged in user
  // Required
  user: {
  },
  
  // The company of the currently logged in user
  company: {
  },

  // Environment. Defaults to production. If you set this
  // to anything other than 'production' then you can use
  // Secure Mode but it will not be forced on. This way
  // You can test it in Development, Staging, etc... before
  // deploying
  // Default: "production"
  environment: "production",




  /*
   * Secure Mode Options
   * Secure Mode is disabled by default. Once enabled, it
   * cannot be turned off.
   */
  // Options for Secure Mode
  ts: 1234567890,
  auth_hash: "mumbo-jumbo",




  /*
   * Misc Options
   */
  // Disables watching `window.location`, and automatically calling
  // .page() when a change (include anchor changes) are noticed.
  // Default: false
  disable_location_watch: false,

  // The ID of a Question you want to force ask
  // Default: null
  question_id: "string-id-of-question",


  // Make RamenJS not log to console
  // Default: false
  silent: false,



  
  /*
   * Product Center Options
   */
  // Custom Trigger Element
  customer_trigger_id: "el-id",

  // Custom Links
  custom_links: [
  ]

};
```

## Ramen.Api.update(config)


```javascript
config = {
  user: {
    id: '34349853',
    name: 'Marky Marcus',
    email: 'ryan+marky@ramen.is'
  }
};

Ramen.Api.update(config);
```
This updates the data for the currently logged in user.

## Ramen.Api.track(event_name)

```html
<a href="/unsubscribe" onclick="Ramen.Api.track('Clicked Unsubscribe Link');">
I'm out.
</a>
```

You can track events using `Ramen.Api.track(event_name)` and then use that data
in Audience creation.

For example, you could create an event called "Clicked Unsubscribe Link",
and have a question appear on the following page.

## Ramen.Api.page()

```javascript
Ramen.Api.page()
```

Notify Ramen that the page has changed. This will trigger
a lookup to see if the new page means the current customer
should be asked a question.

By default, Ramen
will monitor `window.location` for changes, but you
can force this with a call to `.page()`

## Ramen.Api.die()

```javascript
Ramen.Api.die()
```

Kill RamenJS. This will:

* Remove all elements added to the DOM
* Remove all listeners added
* Clear all intervals and timeouts


