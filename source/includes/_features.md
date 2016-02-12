# Features

## The feature object

```shell
EXAMPLE OBJECT

{
  "id": "",
  "object": "feature",
  "created_at": "",
  "updated_at": "",
  "last_active_at": "",
  "project_id": "",
  "phase": "",
  "bucket_id": "",
  "community_member_id": "",
  "name": "",
  "description": "",
  "publicly_visible": "",
  "published_at": "",
  "notified_at": "",
  "archived_at": "",
  "archival_reason": "",
  "tracking_js_key": "",
  "tracking_enabled": "",
  "tracking_url": "",
  "tracking_regex_enabled": "",
  "tracking_url_regex": "",

  // ---- relationships

  "updates":  [], 
  "comments": [],

  // --- ATTRIBUTES TO NOT EXPOSE VIA API

  "original_text": "",
  "sanitized_text": "", 
  "stripped_text": "", 
  "position": "",
  "tags": "",
  "attachment_url": "",
  "from_idea_id": "",
  "instructions_to_find": "",
  "used_by_user_ids": "",
  "source_id": "",
  "projected_delivery_date": "",
  "actual_delivery_date": "",
  "status": ""
}
```

Attribute | Description
----------|------------
** TODO. describe attributes. **


## Create a feature

```shell
```

### Arguments
Parameter | Description
----------|------------
project_id | string. required. Must be a project within the organization.
phase | string. required. Must be one of: "idea", "roadmap", "being-developed", "deployed", "validated".
bucket_id | string. required. Must be a bucket within the project.
community_member_id | string. required. Must be a community_member_id within Ramen organization.
name | string. required.
description | string. required. Can be plain text or valid HTML.
publicly_visible | boolean, true or false. optional. Default true.
tracking_enabled | boolean, true or false. optional. Default false.
tracking_url | string. optional. URI to track feature on your site.
tracking_regex_enabled | boolean, true or false. optional. Default false.
tracking_url_regex | string. optional.

### HTTP Request
`POST /api/v1/projects/:project_id/features`

### HTTP Response
Returns Feature object or error(s).




## List features

### HTTP Request
`GET /api/v1/projects/:project_id/features`


### HTTP Response
Returns an array of Feature objects or error(s).




## Retrieve a feature

### HTTP Request
`GET /api/v1/projects/:project_id/features/:id`

### HTTP Response
Returns Feature object or error(s).




## Update a feature

### HTTP Request
`PUT /api/v1/projects/:project_id/features/:id`

### HTTP Response
Returns an updated Feature object or error(s).




## Delete a feature

### HTTP Request
`DELETE /api/v1/projects/:project_id/features/:id`

### HTTP Response
Returns JSON with deleted object's primary ID.



## List feature comments

### HTTP Request
`GET /api/v1/projects/:project_id/features/:id/comments`

### HTTP Response
Returns an array of <a href="#comments">Comment objects</a> or error(s).



## List feature updates

### HTTP Request
`GET /api/v1/projects/:project_id/features/:id/updates`

### HTTP Response
Returns an array of <a href="#updates">Update objects</a> or error(s).