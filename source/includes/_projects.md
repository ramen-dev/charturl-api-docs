# Project

## The project object

```shell 
EXAMPLE OBJECT

{
  "id": "",
  "object": "project",
  "created_at": "",
  "updated_at": "",
  "name": "",
  "logo_url": "",
  "site_url": "",
  "tagline": "",
  "description": "",
  "location": "",
  "tags": "",
  "tech_tags": "",
  "slug": "",
  "og_share_image_url": "",
  "twitter": "",
  "facebook": "",
  "share_message": "",
  "feature_tags": "",
  "publicly_visible": "",

  // --- ATTRIBUTES TO NOT EXPOSE VIA API

  "plan": "",
  "microwave": "",
  "risks": "",
  "goal_in_cents": "",
  "end_date": "",
  "hero_url": "",
  "noodle_bar_image_url": "",
  "marketplace_sort": "",
  "force_enable_kitchen": "",
  "noodle_bar": "",
  "successful": "",
  "failed": "",
  "video_url": "",
  "video_webm_url": "",
  "discount_percent": "",
  "discount_amount": "",
  "open_invite_enabled": "",
  "kitchen_only": "",
  "ramen_event_received_at": "",
  "priority": "",
  "ask_for_linkedin": ""
}
```

Attribute | Description
----------|------------
** TODO. describe attributes. **

## Create a project

```shell
$ curl \
  -X POST \
  -H "Content-Type: application/json" \
  -H "RAMEN_API_KEY: 123" \
  -d '{ "name": "Ramen API" }' \
  https://ramen.is/api/v1/projects
{
  "name": "Ramen API",
  "id": "545ea888646d6115461d0000",
  "object": "project"
}
```

### HTTP Request
`POST /api/v1/projects`

### Arguments
Parameter           | &nbsp;
------------------- | ---------
name                | required.

### HTTP Response
Returns Project object or raises an error.

## List projects

```shell
$ curl \
  -H "Content-Type: application/json" \
  -H "RAMEN_API_KEY: 123" \
  https://ramen.is/api/v1/projects

[
  {
    "name": "Ramen API",
    "id": "545ea888646d6115461d0000",
    "object": "project"
  },
  {
    "name": "Mobile App",
    "id": "54606182646d61258a030000",
    "object": "project"
  }, 
  {
    "name": "Ramen",
    "id": "54606132646d61258a030000",
    "object": "project"
  }
]
```

```ruby
```

### HTTP Request
`GET /api/v1/projects`

### Arguments 
None.

### HTTP Response
Returns list of Project objects.

## Retrieve a project
```shell
$ curl \
  -H "Content-Type: application/json" \
  -H "RAMEN_API_KEY: 123" \
  https://ramen.is/api/v1/projects/545ea888646d6115461d0000

{
  "name": "Ramen API",
  "id": "545ea888646d6115461d0000",
  "object": "project"
}
```

```ruby
```

### HTTP Request
`GET /api/v1/projects/:id`

### Arguments 
Parameters  | &nbsp;
------------|-------
id          | required.

### HTTP Response
Returns Project object or raises error.

## Update a project
```shell
$ curl \
  -X PUT
  -H "Content-Type: application/json" \
  -H "RAMEN_API_KEY: 123" \
  -d '{ "name": "Ramen API v2"}'
  https://ramen.is/api/v1/projects/545ea888646d6115461d0000

{
  "name": "Ramen API v2",
  "id": "545ea888646d6115461d0000",
  "object": "project"
}
```

```ruby
```

### HTTP Request
`PUT /api/v1/projects/:id`

### Arguments
Same arguments as creating a project. See <a href="#create-a-project">Create a project</a>

### HTTP Response
Returns Project object or raises error.

## Delete a project
```shell
$ curl \
  -X DELETE
  -H "Content-Type: application/json" \
  -H "RAMEN_API_KEY: 123" \
  https://ramen.is/api/v1/project/54606182646d61258a030000

{
  "deleted": "true",
  "id": "54606182646d61258a030000"
}
```

```ruby
```

### HTTP Request
`DELETE /api/v1/projects/:id`

### Arguments
Parameters  | &nbsp;
------------|-------
id          | required.

### HTTP Response
Returns JSON with deleted object's primary ID.
