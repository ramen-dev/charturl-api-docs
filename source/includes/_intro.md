## C3.js

Our charts are drawn by C3.js. C3 was chosen because it is well-maintained, and doesn't use any fancy CSS3 that throws our screenshot software into disarray. The construction of its options argument is very straightforward, and their documentation, while not perfect, is among some of the best for free JS charting libraries.

[Read the C3.js documentation here](http://c3js.org/).

## DataMap

We recently released support for [DataMaps](http://datamaps.github.io/). See our examples page for an example of a Chloropleth chart and how to use this library yourself.


## Templates & Confguration

### Project-level configuration

When you create a Project, you have the option to supply **Config JS Object** and **Custom CSS**. Our Config **JS Object** is structured as follows:

```json
{
  "charturl": {
    "_comment": "ChartURL-specific options.",
    "pixel_ratio": 1  // Can be set to 2 for retina
    "type": null      // Can be set to "datamap" for DataMaps: http://datamaps.github.io
  },

  "options": {
    "_comment": "This becomes the `options` object passed to C3 or DataMaps"
  }
}
```

### Template-level configuration

Templates inherit the **Config JS Object** and **Custom CSS** of their parent projects. They, in turn, have their own **Template Config JS Object** and **Template Custom CSS** that can augment and override the Project-level configuration. They follow the same rules as Project-level configuration.


## Image Details

### Image Formats

Images are returned as `PNG` files.

### iFrame Support

This has had very little testing, but we wanted to see what you would do with it. If you append `.html` on the end of a URL, you'll get back a webpage. You can put this in an iframe and use it how you see fit.

### Image Sizes

Image heights and widths should not be less than 40px. The max height and width is 1200px.

### Retina Image Support

We now support modifying the pixel ratio by setting the `charturl.pixel_ratio` in your Config JS Object.

For ease of use in stylesheets and the srcset attribute, you can also append `retina=1` onto any URL and it will have the same effect as setting the `charturl.pixel_ratio` option.
