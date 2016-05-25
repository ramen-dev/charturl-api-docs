# Setup Guide

This guide will walk you through getting started with ChartURL.

## 1. Create a project

Projects are where you keep all your chart templates and set up your production
and development testing environments. We create your first project for you, and
you can add others as needed. Each project has it’s own `token` (for use in creating
Signed URLs) and it's own `api_key` (for use in creating ShortURLs).

Projects have Project-level settings you can use to maintain consistency. This
can be used to set typography, custom watermarks, and color palettes across
all templates in the project.

## 2. Create a template

Create your first template by heading into a project and clicking ‘Create
Template’

![Create a template](https://www.evernote.com/l/AgUPiXIVTaZGNovv0TNQutpkZcE3PkXbaWUB/image.png)

Give your template a name, and you can start to edit the settings.

### Template Level Configurations

In a template you can add all the code to define how your chart will look. You
will need to create a new template for each unique chart you want to create. 

![Config options](https://www.evernote.com/l/AgX_PwqrupBH6ZdaUxUQbABqYfO-Oh2W3HkB/image.png)

### Config JavaScript Object

The Config JavaScript object is structured as follows:

Attribute | Type | Meaning
---|---|---
charturl|Object|ChartURL options
options|Object|The object passed to the charting library

The Config JS object is JavaScript, which means you can include closures:

`function(v) { return Math.round(v) }`

### Custom CSS

> By default, the `body` is transparent. If sending images to a printer,  change it to white.

```css
body {
  background-color: white;
}
```

Use this CSS to style your chart. C3js relies heavily on CSS for styling, while
ChartJS uses options passed into its constructor to style the chart.

### Template Data for Preview

> Example JSON for Preview

```json
{
  "charturl": { },
  "options": {
    "data": {
     "columns": [["Series 1", 1,2,3,4,5], ["Series 2",2,3,4,5,6]]
    }
  }
}
```

The Preview Data is structured exactly like the Config JS object with one very
big difference. The Preview Data is JSON, not JavaScript. This means object
keys need to be wrapped in double quotes, and closures are not allowed.

This is where you can add example json data to test our your chart. We’ll save
that test data for you to use in the future. If you want to see how some
example test data looks [check out one of our example
templates](https://charturl.com/app/examples).

### Preview the chart

We provide a simple preview so you can see how your chart will look. Clicking
‘Save and Refresh All’ will update this preview. For troubleshooting, you can
also open the HTML version of the chart incase you need to troubleshoot the
code.

### Project Level Configurations

When editing a template you will also be able to edit Project-level
configurations for ‘JS Object’ and ‘Custom CSS’. Keep in mind this will be
applied to ALL of your templates in a project. There is no other place to edit
Project-level settings.

Not sure where to start? [Try one of our
examples](https://charturl.com/app/examples).

## 3. Choosing a charting library

To choose a charting library, you'll want to set the `charturl.type` option to the
appropriate value. Below we list out our charting libraries, show you how to choose
that library, and link to their documentation.

### ChartJS 2.0

We are currently running version 2.0.0. You can find
the documentation for ChartJS here: [ChartJS 2.0 Documentation](https://chartjs.org)

To use ChartJS, set `charturl.type` to `chartjs`.

### DataMaps

DataMaps lets you create charts that look like this:

![Bubbles](https://dl.dropboxusercontent.com/spa/c8k9520tqhih2dg/y-a67_4d.png)

And this:

![Projections](https://dl.dropboxusercontent.com/spa/c8k9520tqhih2dg/4hwi9i1t.png)

And this: 

![Africa](https://dl.dropboxusercontent.com/spa/c8k9520tqhih2dg/fs3bpnnv.png)

It is, in a word, **awesome**.

We are currently running DataMaps version 0.4.0, which you can find here:
[DataMaps Documentation](http://datamaps.github.io)

To use DataMaps, set `charturl.type` to `datamaps`

<aside class="warning">
<code>charturl.type</code> also supports being set to <code>datamap</code without the <code>s</code>
because we typo'd it in some old documentation :)
</aside>

### C3.js

C3.js was the original library supported. To use it, you can leave `charturl.type` blank or set it to `c3js`.

We are currently running version 0.4.10. You can find the documentation for C3js here:
[C3js Documentation](http://c3js.org)

<aside class="warning">
The C3js documentation is not very robust. It also is largely missing all material relating to how to
style charts. For this reason, we <strong>strongly</strongly> recomment using ChartJS.
</aside>

## 4. Understanding how to setup your request-level data

We’ve already covered Project-level configuration (for things like typography,
colors, or custom watermarking) and Template-level configuration (for things
like chart type & chart options). A request to generate a chart will send in
additional information like the data you want to chart, but you can also pass
in other options that override the higher level options. 

### Config JS

The `charturl` and `options` objects get merged together with the project- and
template-level counterparts. Request-level takes precedence over
Template-level, which in turn takes precedence over Project-level.

### Custom CSS

The CSS is rendered into the page in the following order:

- Project-level
- Template-level
- Request-level

### Custom JS [Special pricing tier]

The Custom JS feature is only available at higher pricing tiers. Contact
support if you would like to have this feature enabled.

The JS is first wrapped in an `onready` callback similar to jQuery’s
`$(function() { … })` and then the custom JS blocks are rendered in the
following order:

- Project-level
- Template-level
- Request-level

