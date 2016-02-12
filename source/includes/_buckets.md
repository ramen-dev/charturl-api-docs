# Buckets

## The bucket object

```shell
EXAMPLE OBJECT

{
  "id": "",
  "object": "bucket",
  "created_at": "",
  "updated_at": "",
  "project_id": "",
  "name": "",
  "completion_date": ""

  // --- ATTRIBUTES TO NOT EXPOSE VIA API

  none
}
```

Attribute | Description
----------|------------
** TODO. describe attributes. **


## Create a bucket 

### HTTP Request
`POST /api/v1/projects/:project_id/buckets`

### Arguments 
Parameter | &nbsp;
----------|-------
project_id | required.
name | required.
completion_date | optional.

### HTTP Response
Returns created Bucket object or error(s).



## List buckets

### HTTP Request
`GET /api/v1/projects/:project_id/buckets`

### HTTP Response
Returns an array of Bucket objects or error(s).



## Retrive a bucket

### HTTP Request
`GET /api/v1/projects/:project_id/buckets/:id`

### HTTP Response
Returns Bucket object or error(s).



## Update a bucket

### HTTP Request
`PUT /api/v1/projects/:project_id/buckets/:id`

### HTTP Response
Returns updated Bucket object or error(s).



## Delete a bucket

### HTTP Request
`DELETE /api/v1/projects/:project_id/buckets/:id`

### HTTP Response
Returns JSON with deleted buckets's id.
