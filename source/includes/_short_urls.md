# Short URLs

## What are Short URLs?

### How to Use
Short URLs are for when you have too much data to fit into the 2,000 character limit of a GET string. You POST the data to us, and we'll return a Short URL for you to use.

### They're Free
You do not get charged for an "image" when creating a Short URL.

### They're Fast
Since we don't render the image until the resulting Short URL is used within an `img` tag, so this endpoint is very speedy. If you're seeing response times over 20ms, contact [support](mailto:support@charturl.com) because something is awry.


### Example
Below is a heavily documented Ruby example of creating a Short URL


```ruby
=begin
Creating your first Short URL
This heavily commented Ruby example will walk you through
creating your first Short URL for ChartURL
First, you're going to need to get some things from your account
`api_key`
This is found under the Project. We provide two API keys: one
for your production environment and one for development. The
development key will always return images that are watermarked
with an ugly "CHARTURL PREVIEW", but you'll never be charged
for those images (either overage fees or credits against your plan).
For this example, we'll use "dak-55045dac-bb35-40ac-80c8-874ab71c6f83"
for an `api_key`, which is a real development key we use for
these examples.
`template_slug`
Templates hold all the config options you want your chart to have.
When creating a Short URL, you can reference a `template_slug`, and
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

# We need to make an HTTP request. We're not big fans of Net::HTTP
# (the standard library that comes with Ruby) so we've already
# installed the Typhoeus Gem https://github.com/typhoeus/typhoeus
require 'typhoeus'

# Set our API Key. You'll probably want to set this conditionally
# based on environment so that you use your development keys and
# not get charged while in non-production (dev/test/staging/qa)
API_KEY = "dak-55045dac-bb35-40ac-80c8-874ab71c6f83"

# We'll define a helper method to generate the URLs. It'll take
# two arguments: `template_slug` (which will be "weekly-activity")
# and `options` (which will be our data)
def charturl_url(template_slug, options)

  # The endpoint for creating a ShortURL is:
  #   "https://charturo.com/short-urls.json"
  #
  # You need to add the `api_key` query string parameter to
  # identify and authenticate yourself
  #
  # ALWAYS USE "HTTPS". If you don't, you will get a 302
  # redirect response from our endpoint, and you will have
  # exposed your API key to the outside world.
  url = "https://charturl.com/short-urls.json?api_key=#{API_KEY}"

  # You need to pass along the 'application/json' header or else
  # our API will return a 400 Bad Request response.
  headers = {
    'Content-Type' => 'application/json'
  }

  # The body of our post will contain the `template_slug` and our
  # options. We'll generate a Ruby hash, convert it to JSON,
  # and use that string as our body.
  body = {
    template: template_slug,
    options: options
  }.to_json

  # Make the request to create a ShortURL
  surl_response = Typhoeus::Request.post(url, body: body, headers: headers)

  # Always check for errors
  if !surl_response.success?
    raise("Error creating ShortURL: #{surl_response.inspect}")
  end

  # response.body will look like this: '{"short_url": "https://charturl.com/r/38ag"}'
  # Parse the JSON
  parsed_body = JSON.parse(surl_response.body)

  # parsed_body is now a Ruby Hash object
  # Return the URL
  return parsed_body['short_url']
end

# Call our helper
url = charturl_url("weekly-activity", data: {columns: [["This week", 4,1,5,6,1,7,8], ["Last week", 1,5,3,1,6,2,6]]})
url #=> "https://charturl.com/r/J9lA"

# Use the URL in an HTML5 image tag
#
#   <img src="https://charturl.com/r/J9lA">
```
