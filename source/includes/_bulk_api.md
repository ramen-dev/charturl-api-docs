# Bulk API


The Bulk API is just like the [Short URL](/#short_urls) API, but instead of sending us data for one chart at a time, you can send up to 1,000.

The request is sent via POST just like the [Short URL API](/#short_urls), and a JSON response returned.

## Requirements
The id must be a string, but it can be a number string like "1".
The id must be unique, but only within the scope of request, so you can use incrementing integers from "1" to "100" in all your requests.
Beyond checking your API key and verifying that the string you passed is valid JSON, we don't do any validation, so be careful with what you send us.

Want to use the Bulk API?
Contact us by emailing [support@charturl.com](mailto:support@charturl.com) if you would like access to the bulk API.

```shell
#
# HTTP request body
#

[
  {
    "id": "1",
    "template": "quick-pie",
    "charturl":{},
    "options":{"data": {"columns": [["Yes", 2], ["No", 3], ["Unsure", 6]]}, "size": {"width": 200}}
  },
  {
    "id": "2",
    "template": "weekly-activity",
    "charturl":{},
    "options":{"data": {"columns": [["Last Week", 1,2,3,4,3,2,1], ["This Week", 22,5,1,5,1,5,6]]}}
  }
]


#
# HTTP response body
#

{
  "short_urls": {
    "1": "https://charturl.com/r/R89H",
    "2": "https://charturl.com/r/lNnu",
  }
}
```
