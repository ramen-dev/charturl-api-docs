# Image Details

### Image Formats

Images are returned as PNG files. Support for TIFF is coming soon.

### Image Sizes

Image heights and widths should not be less than 40px. The max height and width
is 1200px. To specify height & width, look at the documentation for the
charting library you are using.

### Retina Image Support

We now support modifying the pixel ratio in two ways. First, you can set the
`charturl.pixel_ratio` in your Config JS Object. See the [Config JavaScript
Reference](#config-javascript-reference) below for more information. Second,
you can add the `retina=1` parameter to any URL (Signed or Short) and a
retina-scale image will be returned.

For ease of use in stylesheets and the srcset attribute, you can also append
retina=1 onto any URL and it will have the same effect as setting the
charturl.pixel_ratio option.

### Using `srcset`

The `srcset` attribute is a handy way to provide retina resolution options to
browsers without making them download both versions of the image. Below is an
example of how to use `srcset`

`<img src="[url]" srcset="[url],1x [url]?retina=1 2x">`

Using `srcset` and our `retina=1` option will greatly increase the quality of
your ChartURL images on retina screens. For more information about `srcset`
[check out this article at CSS-TRICKS](https://css-tricks.com/srcset-chrome/).

### Asset Storage

We store all images on S3.

### Loading Speed

Size of the image and network speeds will obviously have an impact, but an
800x400 PNG will render on our end in around 400ms.

### ChartURL Watermark Branding

The ChartURL watermark branding on images is removed once you choose any paid
plan.

### Custom Watermark Branding

```css
body:before {
  content: " ";
  display: block;
  position: absolute;
  right: 0;
  bottom: 0;
  height: 20%; 
  width: 40%;
  z-index: -1;
  opacity: 0.2;
  background: url(/* DATA URI */);
  background-size: contain;
  background-position: bottom right;
  max-height: 40px;
  max-width: 120px;
}
```

We support custom watermark branding using CSS and an image data URI. See the
example CSS on the right. We recommend setting `max-width` and `max-height` to
the size the image to avoid it looking blurry on larger images. Your logo
should be a PNG with a transparent background. To turn your image into a data
URI, use a service [like this one](http://dopiaza.org/tools/datauri/index.php).

Technically, you could use an external URL (to an asset on S3 for example) in
place of the `background-url`, but **do not do that**.  We cannot guarantee the
images will load correctly at scale.

### Caching image URLs

You'll notice that the URLs you generate redirect to S3 urls. Do not store these S3 URLs, as
we do not guarantee they will not change over time.
