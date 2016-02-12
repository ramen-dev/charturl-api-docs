# Authentication

```shell
$ curl \
  -H "Content-Type: application/json" \
  -H "RAMEN_API_KEY: 123" \
  https://ramen.is/api/v1/....
```

```ruby
Ramen.api_key = "your_api_key"
```

Ramen uses API keys to authenticate API requests. 

You can create and revoke API Keys within each Organization on the API keys 
page, `https://your-organization.ramen.is/api_keys`. The Api Key will allow 
you to interact with all objects within that organization.
