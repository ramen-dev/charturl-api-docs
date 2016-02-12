# Community Members

## The community member object

```shell
{ 
  "id", 
  "object": "community_member",
  "created_at": "", 
  "updated_at": "", 
  "joined_at": "",
  "type": "",
  "title": "",
  "short_bio": "",
  "last_active_at": "",
  "segments": "",

  // --- ATTRIBUTES TO NOT EXPOSE VIA API

  "level": "",
  "value": "",
  "project_ids": "",
  "gates": "",
  "last_app_active_at": ""
}
```

Attribute | Description
----------|------------
** TODO. describe attributes. **



## Create a community member

Community Members are created when a user accepts an invitation. Therefore,
to create a community member you'll need to invite them to join you on the
Ramen platform. Check out <a href="#create-an-invitation">creating invitations.</a>



## List all community members

### HTTP Request
`GET /api/v1/community_members`

### HTTP Response
Returns an array of Community Member objects or error(s).



## Retrieve a community member

### HTTP Request 
`GET /api/v1/community_members/:id`

### HTTP Response
Returns Community Member object or error(s).



## Update a community member

### HTTP Request 
`PUT /api/v1/community_members/:id`

### HTTP Response
Returns an updated Community Member object or error(s).



## Delete a community member

### HTTP Request 
`DELETE /api/v1/community_members/:id`

### HTTP Response
Returns JSON with deleted Community Members's id.
