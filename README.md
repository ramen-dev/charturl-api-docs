# ChartURL API Docs

We're using [Slate](https://github.com/tripit/slate) to generate beautiful API docs.

## Development

To get started,

    git clone git@github.com:ramen-dev/charturl-api-docs.git
    cd charturl-api-docs
    bundle install

You can run a local version of the docs site via the `middleman server` by running,

    middleman server

And going to [0.0.0.0:4567](http://0.0.0.0:4567/)

## Deployment

We're using Github pages to host the API docs.

Therefore to publish the docs you run,

    rake publish

And changes will be published/deployed to [docs.charturl.com](http://docs.charturl.com/)
