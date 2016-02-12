# (Deprecated) Encrypted URLs

This method is deprecated. If you're already using this method, feel free to keep using it, but new users should not user it. It works just fine, but the [Signed URL](/#signed-urls) method is easier to implement and just as secure.

## How to Use Encrypted URLs

Encrypted URLs let you construct a URL on the fly that will instantly be turned into an image when used in an `img` tag.

### Why Encrypted?

Encryption is the only way we can guarantee someone else isn't using your account and running up your bill.

### Pros to Encrypted URLs

It's quick. You generate a URL on your server, and then use it in an `img` tag.

### Cons to using Encrypted URLs

URLs can only be ~2,000 characters. Furthermore, when sending HTML emails, some services will proxy images, making the URLs even longer. This is a problem that manifests inside the browser or e-mail client, so there's no way for you to even know that your user is seeing a broken image.

## Generating the URL

```ruby
=begin
Creating your first Encrypted URL
This heavily commented Ruby example will walk you through
creating your first Encrypted URL for ChartURL
First, you're going to need to get some things from your account
`encrypt_key`
This is found under the Project. We provide two encrypt keys: one
for your production environment and one for development. The
development encrypt key will always return images that are watermarked
with an ugly "CHARTURL PREVIEW", but you'll never be charged
for those images (either overage fees or credits against your plan).
For this example, we'll use
"dek-d7a46236eda961a6c3c18ffcc6b077ba87d27e9ae85f7842c6d427c265dd5f69d5131308d93332353d4a55a4b1160fcf516515a4a9f0aa50fbf2d7a2e7d0f1c5"
for an `encrypt_key`, which is a real development key we use for
these examples.
`token`
This is also found under Project. We'll use "dt-RwYN" for our
`token`.
`template_slug`
Templates hold all the config options you want your chart to have.
When creating an Encrypted URL, you can reference a `template_slug`, and
just pass in the data that you want rendered in that template.
When you pass in the data for the chart, you can optionally pass in
options that can augment or override the settings store in your template.
We've created several templates for you including:
* "quick-pie": A simple pie chart
* "weekly-activity": A bar chart with X-axis labels of "M" through "Su"
* "timeseries": A line chart that can accept timestamped data
For this example, we'll use "weekly-activity" for `template_slug`
=end

# We need to convert stuff to JSON. In Ruby 2.1.2, 'json' is part of
# the standard library. You may need to install a rubygem for earlier
# versions of Ruby
require 'json'


# We encrypt the data to prevent other people from using your account.
# The cipher we use is AES-256-CBC, which is a very secure, standard
# encryption cipher. There are libraries in most languages that will
# do all the heavily lifting for you. Ruby comes with such a library,
# OpenSSL::Cipher
require 'openssl'


# We need to Base64 encode the encrypted data. Ruby comes with a
# Base64 library
require 'base64'


# To construct the final URL, we'll need to CGI escape some things
require 'cgi'



# Set our Encrupt key & Token. You'll probably want to set this conditionally
# based on environment so that you use your development keys and
# not get charged while in non-production (dev/test/staging/qa)
ENCRYPT_KEY = "dek-d7a46236eda961a6c3c18ffcc6b077ba87d27e9ae85f7842c6d427c265dd5f69d5131308d93332353d4a55a4b1160fcf516515a4a9f0aa50fbf2d7a2e7d0f1c5"
ENCRYPT_KEY_DIGEST = KEY_DIGEST = OpenSSL::Digest::SHA256.new(ENCRYPT_KEY).digest
PROJECT_TOKEN = "dt-RwYN"

# We'll define a helper method to generate the URLs. It'll take
# two arguments: `template_slug` (which will be "weekly-activity")
# and `options` (which will be our data)
def charturl_url(template_slug, data)

  # The JSON should have the following structure:
  # {
  #   "options": {
  #     # C3.js options. See http://c3js.org
  #   }
  # }
  json = {options: data}.to_json


  # We use the AES-256-CBC cipher
  # Make sure to generate a random IV each time
  cipher = OpenSSL::Cipher.new 'AES-256-CBC'
  cipher.encrypt
  iv = cipher.random_iv
  cipher.key = ENCRYPT_KEY_DIGEST
  encrypted_json = cipher.update(json) + cipher.final

  # Since we're sending the IV and the data along in the URL,
  # they both need to be Base64 encoded and then CGI escaped.
  # Note that your IV might be a hex string, which doesn't need
  # to be Base64 encoded. However, some libraries generate IVs
  # that are not Base64-compatible, so to keep things consistent,
  # we always Base64 _DECODE_ the IV on our end. Therefore, you
  # need to Base64 ENCODE it or else you'll see "Decrypt Error"
  iv_for_url = CGI.escape(Base64.encode64(iv))
  data_for_url = CGI.escape(Base64.encode64(encrypted_json))

  url = "https://charturl.com/i/#{PROJECT_TOKEN}/#{template_slug}/#{iv_for_url}/#{data_for_url}"

  # Check to see if URLs are too long
  if url.size > 2083
    # Instead of raising an exception, you could call another
    # helper that generates a ShortURL
    raise "URL too long. Switch to ShortURL"
  end


  # OPTIONALLY check this soft limit
  if url.size > 1500
    raise "URL is getting too close to limit. Images may not render in mail clients"
  end


  # Return URL
  return url
end

# Call our helper
url = charturl_url("weekly-activity",
    data: {columns: [["This Week", 10,12,41,9,14,15,15], ["Last Week", 9,14,21,21,20,3,5]]})
url

# ^ If you run this command multiple times, you'll get different URLs. This is
# because of the IVs being random.
```
