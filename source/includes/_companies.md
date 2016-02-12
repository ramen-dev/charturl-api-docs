# Companies

```html
<script>
  window.ramenSettings = {
    organization_id: "83hakj3",
    user: { /* Explained above */ },
    company: {
      id: "42",
      name: "Ramen",
      url: "https://ramen.is"
      value: 353000.0,
      traits: {
        is_rad: true
      }
    }
  };
</script>
```

You can group a Customer into a Company. A Company is
an organization that the currently logged in person
belongs to.

Company data can be used when creating
[Audiences](#audiences). So you could, for example,
target a question to only appear to Customers that
are members of a specific Company.

RamenJS wants to know the following things
about Companies:

Attribute | Type | Required | Notes
--- | --- | --- | ---
id        | String  | Yes | A unique identifier
url       | String  | Yes | A valid URL for the comapny
name      | String  | Yes | The name of the company
value     | Float   | No  | An arbitrary value for that company. Used for Audience creation.
traits    | Object  | No  | See [Custom Traits](#custom-traits) below



