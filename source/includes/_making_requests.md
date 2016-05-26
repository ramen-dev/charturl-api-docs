# Creating Chart URLs 

We support 2 different methods for generating image URLs.
Read below about ShortURLs and Signed URLs to choose the
method that is right for you.

Constructing a URL is *free* and *fast*. Since you don't get charged until
an image is viewed, you can create as many of these as you want.

## Preferred Method: ShortURLs

ShortURLs are preferred since they completely remove the chances of running up
against the ~1,500 character limit on GET strings.

This method lets you POST us as much data as you want and get back a short
URL like this: `https://charturl.com/r/nXN2`

### The ShortURL endpoint is designed to be fast

Since we don’t render the image until the resulting ShortURL is used within an
`img` tag, this endpoint is very speedy. If you see response times over
20ms, contact support because something is awry.

In order to keep this endpoint fast, we don't do any validation on the data you send us.
You could send along a non-existant Template slug or you could have a typo in your JSON
config, but the ShortURL endpoint would still return a 201 status code and a
ShortURL regardless. Keep this is mind and be sure to test your ShortURLs before deploying them into
production.

For details on how to create a ShortURL, see the [ShortURL Reference](#shorturl-reference) below.

## Secondary Method: Signed URLs

> An example Signed URL

```
https://charturl.com/i/9yi1/area-spline?d=%7B%22options%22%3A%7B%22data%22%3A%7B%22columns%22%3A%5B%5B%22Revenue+in+%24%22%2C300%2C350%2C300%2C0%2C0%2C0%5D%2C%5B%22Customers%22%2C130%2C100%2C140%2C200%2C150%2C50%5D%5D%7D%7D%7D&s=cw7R0Nlj2VB1kYvdLF1A9h%2BICpAQ0PThzWdUE4OPohg%3D%0A
```

Signed URLs let you construct a URL on the fly that will instantly be turned
into an image when used in an img tag. This method limits the amount of data
you can send, since URLs have a max length, but here is an example URL:


Signed URLs are helpful when you can't afford to wait for the network latency
of making a call to our ShortURL endpoint.

For details on how to create a Signed URL,
see the [Signed URL Reference](#signed-url-reference) below.
