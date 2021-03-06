# Introduction

> Ruby assumes at least version 2.1. JavaScript is mostly targeted at NodeJS examples.

ChartURL is a product that enables you to turn your data into image charts for emails,
reports, chat bots, & web/mobile apps. We support several charting libraries. We
fully expose the API for all the charting libraries we support, so anything you can do with
those Charts on the web can be done with ChartURL.

### Libraries

- [ChartsJS](http://chartjs.org)
- [Datamaps](http://datamaps.github.io)
- [C3.js](http://c3js.org)

# Who are these docs for?

This is the documentation for the ChartURL Developer API. If you are looking for help with the
ChartURL for Marketers product, please [contact support](mailto:support@charturl.com).

Don’t know what product to use? If your desired use case is that you want to upload a data file to
ChartURL and get back a file that includes links to images, then you want to use the Marketer product.

# Use Cases

### Email

Embedding charts in emails is the most common use case for using ChartURL.
There is no reliable way to have consistent looking charts in email without
rendering them as an image.

### Chat bots

JavaScript charting libraries don’t run in chat systems like Slack and Hipchat,
but those products do let you embed images, and that's all that is needed for ChartURL to work.
Companies like [Statsbot](http://statsbot.co/) power their Slackbot chat charts
with ChartURL.

![Statsbot](https://dl.dropboxusercontent.com/spa/c8k9520tqhih2dg/giljeau3.png)

### PDF

Some charting libraries do not render correctly in PDFs, so some of our
customers use ChartURL to render charts into custom PDF reports they create for
their customers.

<aside class="notice">
**Note:** When rendering images for PDF, make sure to use our Retina Support
feature, as some of our customers have discovered the 2x pixel ratio is
required to make the images look awesome in their PDFs.
</aside>

### Mobile & Web

Many people want to have charts that look consistent in their company  emails,
their website, and their mobile apps. ChartURL is an easy way to ensure that
consistency. 

This is especially handy for mobile app developers who don’t want to build out
a custom charting solution for their application.
