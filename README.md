# Public documentation

This holds the source for the [docs.yourbase.io][docs.yourbase.io] site. It is
automatically deployed on merges to `main`.

## Running locally

To run docs locally, use

```sh
yb exec
```

or to run without `yb`,

```sh
bundle install
bundle exec jekyll serve --livereload --config _config.yml,_config_dev.yml
```

[docs.yourbase.io]: https://docs.yourbase.io
