# Organization

## The organization object

```shell
EXAMPLE OBJECT

{
  "id" : "", 
  "object": "",
  "create_at": "", 
  "updated_at": "",  
  "site_url": "", 
  "cname": "", 
  "publicly_visible": "", 
  "trial_end_date": "", 
  "plan": "", 
  "open_invite_enabled": "",

  // --- ATTRIBUTES TO NOT EXPOSE VIA API

  "user_id": "", 
  "logo": ""
}
```

Attribute           | Description
--------------------|------------
** rough draft. see example object. **

## Retrieve an organization

```shell
$ curl \
  -H "Content-Type: application/json" \
  -H "RAMEN_API_KEY: abc" \
  https://ramen.is/api/v1/organization
```

```ruby
```

### HTTP Request
`GET /api/v1/organization`

### HTTP Response
Returns an Organization object or error(s).


## Update an orgnization 

```shell
```

```ruby
```

### HTTP Request
`PUT /api/v1/organization`

### HTTP Response
Returns an updated Organization object or error(s).
