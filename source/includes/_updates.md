# Updates

## The update object

```shell
EXAMPLE OBJECT

{
  "id": "", 
  "object": "update",
  "created_at": "", 
  "updated_at": "",
  "project_id": "", 
  "feature_id": "", 
  "title": "", 
  "description": "",
  "publicly_visible": ""
  "notified_at": ""

  // --- ATTRIBUTES TO NOT EXPOSE VIA API

  none
}
```

Attribute | Description 
----------|------------
** TODO. describe attributes. **

## Create an update

### HTTP Request
`POST /api/v1/projects/:project_id/updates`

### Arguments
Attribute | &nbsp;
----------|-------
project_id | required.
feature_id | optional.
title | required. 
description | required.

### HTTP Response
Returns created update object or error(s).



## List all updates

### HTTP Request
`GET /api/v1/projects/:project_id/updates`

### HTTP Response
Returns array of update objects or error(s).



## Retrieve an update

### HTTP Request
`GET /api/v1/projects/:project_id/updates/:id`

### HTTP Response
Returns update object or error(s).



## Update an update

### HTTP Request
`PUT /api/v1/projects/:project_id/updates/:id`

### HTTP Response 
Returns updated update object or error(s).



## Delete an update

### HTTP Request
`DELETE /api/v1/projects/:project_id/updates/:id`

### HTTP Response
Returns JSON with deleted update's id.
