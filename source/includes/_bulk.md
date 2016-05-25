## Bulk API Reference

> Below is an example JSON body to include in the Bulk API POST

```json
[
  {
    "id": "1",
    "template": "quick-pie",
    "charturl":{},
    "options":{
      "data": {
        "columns": [
          ["Yes", 2],
          ["No", 3],
          ["Unsure", 6]
        ]
      },
      "size": {"width": 200}
    }
  },
  {
    "id": "2",
    "template": "weekly-activity",
    "charturl":{},
    "options":{
      "data": {
        "columns": [
          ["Last Week", 1,2,3,4,3,2,1],
          ["This Week", 22,5,1,5,1,5,6]
        ]
      }
    }
  }
]
```

This endpoint, which is only available at higher pricing tiers,
enables you to create up to 100 ShortURLs at once.

### HTTP Request

`POST https://charturl.com/short-urls/bulk.json`

### Query Parameters

Key | Value
---|---
`api_key`|Your API key for the project your template belongs to


### Headers

Header | Values
--- | ---
`Content-Type`|`application/json`

### Body

The POST body is a JSON array of ShortURL objects. The ShortURL objects are the same as above,
with one exception: the addition of an `id` field. Each member of the array must have a unique
`id` field, so you can use the strings `"1"` to `"100"` for example.


### Response

> Below is an example JSON response from the ShortURL endpoint

```json
{
  "short_urls": {
    "1": {"short_url": "https://charturl.com/r/23425"},
    "2": {"short_url": "https://charturl.com/r/a338h"}
  }
}
```

Responses from the Bulk API  endpoint are always JSON.
