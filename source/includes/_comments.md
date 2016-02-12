# Comments

## The comment object

```shell
EXAMPLE OBJECT 

{
  "id": "", 
  "object": "comment",
  "created_at": "", 
  "updated_at": "",
  "project_id": "", 
  "feature_id": "", 
  "original_text": "",
  "display_text", "",
  "publicly_visible": "",
  "community_member_id": "", 

  // --- ATTRIBUTES TO NOT EXPOSE VIA API

  "comment_thread_id": "",
  "link_target_id": "",
  "link_target_type": ""
}

Attribute | Description 
----------|------------
** TODO. describe attributes. **

```

## Retrieve a comment

### HTTP Request
`GET /api/v1/comments/:id`

### HTTP Response
Returns Comment object or error(s).
