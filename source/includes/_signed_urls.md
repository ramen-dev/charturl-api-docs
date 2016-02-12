# Signed URLs


## What are signed URLs?
Signed URLs let you construct a URL on the fly that will instantly be turned into an image when used in an `img` tag.

### Why Signed?
It helps to ensure that someone else isn't using your account and running up your bill.

### Pros to Signed URLs

It's quick. You generate a URL on your server, and then use it in an img tag.

### Cons to using Signed URLs

URLs can only be ~2,000 characters. Furthermore, when sending HTML emails, some services will proxy images, making the URLs even longer. This is a problem that manifests inside the browser or e-mail client, so there's no way for you to even know that your user is seeing a broken image.



## Generating the URL
The steps are simple:
- Convert your options to JSON.
- Generate an HMAC-SHA256 digest using your "Encrypt Key."
- Base64 encode the digest to generate the signature.
- Encode the data into the URL structure shown below in the Ruby example.

Below is an example in Ruby. You can find examples of calculating an HMAC-SHA256 signature in other languages here: HMAC-SHA256 in Other Languages

```ruby
# This is a working example.
require 'json'
require 'openssl'
require 'base64'
require 'cgi'

ENCRYPT_KEY = "dek-d7a46236eda961a6c3c18ffcc6b077ba87d27e9ae85f7842c6d427c265dd5f69d5131308d93332353d4a55a4b1160fcf516515a4a9f0aa50fbf2d7a2e7d0f1c5"
PROJECT_TOKEN = "dt-RwYN"

def charturl_url(template_slug, options)
  json = options.to_json
  sig = Base64.encode64(OpenSSL::HMAC.digest('sha256', ENCRYPT_KEY, json))

  "https://charturl.com/i/#{PROJECT_TOKEN}/#{template_slug}?d=#{CGI.escape json}&s=#{CGI.escape sig}"
end

# Call our helper
url = charturl_url("weekly-activity",
    {options: {data: {columns: [["This Week", 10,12,41,9,14,15,15], ["Last Week", 9,14,21,21,20,3,5]]}}})
```
