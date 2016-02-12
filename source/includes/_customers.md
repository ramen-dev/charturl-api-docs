# Customers

```html
<script>
  window.ramenSettings = {
    organization_id: "lkadjf89383hr89",
    user: {
      id: "903849h",
      name: "Bugs Bunny",
      email: "ryan+bugs@ramen.is"
    }
  };
</script>
```

Ramen is used for asking questions, but only of your
_users_. This means that until a User has logged into
your app, there is no way Ramen will be able to
interact with them.

In Ramen terminology, a we call a person logged into
you application a 'Customer'.

RamenJS *must* know the following things about your customers:

Attribute | Type | Required | Notes
--- | --- | --- | ---
id        | String  | Yes | A unique identifier
email     | String  | Yes | A valid email address
name      | String  | Yes | The name of the person

In additional, `ramenSettings` also accepts the following options:

Attribute | Type | Required | Notes
--- | --- | --- | ---
created_at | Integer | No | The unix timestamp (epoch seconds, not milliseconds) for when this account was created. 
value     | Float   | No  | An arbitrary value for that person. Used for Audience creation.
traits    | Object  | No  | See [Custom Traits](#custom-traits) below
bug_image_url | String | No | URL for an image to replace the standard green Ramen 'R' icon. See [Customization](#customization) below.
question_id | String | No | The ID of a question. This will forces a specific question to appear no matter what.


