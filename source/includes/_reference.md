# Reference

## ShortURL Reference

> Below is a full example of what you can pass into the ShortURL endpoint

```json
{
  "template": "weekly-activity",

  "charturl": {
    "pixel_ratio": 1,
    "title": {"text": "My great title!"}
  },

  "options": {
    "data": {
      "columns": [
        ["data 1",1,2,3,4],
        ["data 2",2,3,4,5]
      ]
    }
  },

  "custom_css": "body {background-color: black}",

  "custom_js": "/* Some JS */"
}
```

> Code examples for generating ShortURLs

```ruby
require 'typhoeus'
require 'json'

url = "https://charturl.com/short-urls.json?api_key=[REDACT]"
data = {
  template: "weekly-activity",
  options: {
    data: {
      "columns": [
        ["data 1",1,2,3,4],
        ["data 2",2,3,4,5]
      ] 
    }
  }
}

options = {
  headers: {'Content-Type' => 'application/json'},
  body: data.to_json
}

resp = Typhoeus::Request.post(url, options)

JSON.parse(resp)['short_url']  #=> "https://charturl.com/r/23425"
```

```javascript
const https = require('https');

var body = JSON.stringify({
  template: 'weekly-activity',
  options: {
    data: {
      columns: [["x", "2016-01-10", "2016-01-11", "2016-01-12"], ["Steps", 1000, 1200, 1100]]
    }
  }
});

var options = {
  hostname: 'charturl.com',
  port: 443,
  path: '/short-urls.json?api_key=[REDACTED]',
  method: 'POST',
  headers: {
    "Content-Type": "application/json",
    "Content-Length": Buffer.byteLength(body)
  }
};

var req = https.request(options, (res) => {
  console.log('statusCode: ', res.statusCode);
  console.log('headers: ', res.headers);

  res.on('data', (d) => {
    process.stdout.write(d);
  });
});

req.end(body);

req.on('error', (e) => {
  console.error(e);
});

```

```php
<?php

$api_key = "dak-55045dac-bb35-40ac-80c8-874ab71c6f83";
$url = 'https://charturl.com/short-urls.json?api_key=' . $api_key;

# Use `json_encode` to encode your own object into JSON
$content = '{"template": "weekly-activity", "options":{"data":{"columns":[["This Week",10,12,41,9,14,15,15],["Last Week",9,14,21,21,20,3,5]]}}}';

$curl = curl_init($url);
curl_setopt($curl, CURLOPT_HEADER, false);
curl_setopt($curl, CURLOPT_RETURNTRANSFER, true);
curl_setopt($curl, CURLOPT_HTTPHEADER,
        array("Content-type: application/json"));
curl_setopt($curl, CURLOPT_POST, true);
curl_setopt($curl, CURLOPT_POSTFIELDS, $content);

$json_response = curl_exec($curl);

$status = curl_getinfo($curl, CURLINFO_HTTP_CODE);

if ( $status != 201 ) {
    die("Error: call to URL $url failed with status $status, response $json_response, curl_error " . curl_error($curl) . ", curl_errno " . curl_errno($curl));
}

curl_close($curl);

$response = json_decode($json_response, true);

echo $response;
?>


```

This endpoint takes an API key, some data, and creates a ShortURL.

### HTTP Request

`POST https://charturl.com/short-urls.json`

### Query Parameters

Key | Value
---|---
`api_key`|Your API key for the project your template belongs to


### Headers

Header | Values
--- | ---
`Content-Type`|`application/json`

### Body

The POST body is JSON with the following attributes. To the right is an example dataset.

Attribute|Required|Type|Description
---|---|---|---
charturl|No|Object|ChartURL specific options
charturl.type|No|String|Possible values: `chartjs`, `datamaps`, `c3js`. Default: `c3js`
charturl.pixel_ratio|Integer|Possible values: `1`, `2`. Default: `2`
charturl.title|Object|Add a title
charturl.title.text|String|The title text. Default: `(none)`
template|Yes|String|The slug of a template to apply these data to
options|No|Object|This is the object passed to the charting library after merged with the Project- and Template-level ConfigJS settings
custom_css|No|String|CSS to be rendered into the page before storing the image
custom_js|No|String|JavaScript to be executed after the chart loads and before storing the image

### Response

> Below is an example JSON response from the ShortURL endpoint

```json
{
  "short_url": "https://charturl.com/r/23425"
}
```

Responses from the ShortURL endpoint are always JSON.


## Signed URL Reference

> Code examples for generating signed URLs

```php
<?php
# The constants needed
$key = "dek-d7a46236eda961a6c3c18ffcc6b077ba87d27e9ae85f7842c6d427c265dd5f69d5131308d93332353d4a55a4b1160fcf516515a4a9f0aa50fbf2d7a2e7d0f1c5";
$token = "dt-RwYN";
$slug = "weekly-activity";

# The data converted to JSON
$json = '{"options":{"data":{"columns":[["This Week",10,12,41,9,14,15,15],["Last Week",9,14,21,21,20,3,5]]}}}';

# Generating the signature: http://www.jokecamp.com/blog/examples-of-creating-base64-hashes-using-hmac-sha256-in-different-languages/#php
$raw_sig = hash_hmac('sha256', $json, $key, true);
$encoded_sig = base64_encode($raw_sig);
$url = "https://charturl.com/i/" . $token . "/" . $slug . "?d=" . urlencode($json) . "&s=" . urlencode($encoded_sig);

echo '<img src="' . $url . '">';
?>
```

```ruby

require 'json'
require 'typhoeus'
require 'openssl'
require 'base64'
require 'cgi'

key = "dek-d7a46236eda961a6c3c18ffcc6b077ba87d27e9ae85f7842c6d427c265dd5f69d5131308d93332353d4a55a4b1160fcf516515a4a9f0aa50fbf2d7a2e7d0f1c5";
token = "dt-RwYN";
slug = "weekly-activity";
data = { options: {data: {columns: [["This Week",10,12,41,9,14,15,15],["Last Week",9,14,21,21,20,3,5]]}}};
json = data.to_json

# Generating the signature: http://www.jokecamp.com/blog/examples-of-creating-base64-hashes-using-hmac-sha256-in-different-languages/#php
sig = Base64.encode64(OpenSSL::HMAC.digest('sha256', key, json))  


url = "https://charturl.com/#{token}/#{slug}?d=#{CGI.escape(json)}&s=#{CGI.escape sig}"
```

```javascript
```

This endpoint requires two parameters, the JSON data being passed in, and a Signature to ensure authenticity.

### HTTP Request

`GET https://charturl.com/i/[:project_token]/[:template_slug]`

The `project_token` is taken from your Project. The `template_slug` is for your template. Format defaults to PNG, which is currently the only option.

### Query Parameters

Key | Required |Value
---|---|---
`d`|Yes|The CGI-escaped JSON data for your chart
`s`|Yes|A CGI-escaped, Base64-encoded SHA-256 HMAC digest of your `d` parameter and your `ENCRYPT_KEY`
`retina`|No|Include `retina=1` on query string to return 2x resolution image. Do not include parameter on query string to return default image.

### Response

The response will be an image of the desired format.
