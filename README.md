# Perforce Buildkite Plugin [![Build Status](https://travis-ci.com/ca-johnson/perforce-buildkite-plugin.svg?branch=master)](https://travis-ci.com/ca-johnson/perforce-buildkite-plugin)

A [Buildkite plugin](https://buildkite.com/docs/agent/v3/plugins) that lets you check out code from [Perforce Version Control](https://www.perforce.com/products/helix-core)

* Configure by setting env vars in your build environment (e.g. `P4PORT`, `P4USER`) or via plugin config.
* Optionally add workspace mapping.

## Example

Assuming everything is configured via env vars and you just want to sync the whole repository:

```yaml
steps:
    plugins:
      - ca-johnson/perforce: ~
```

Doing configuration via the plugin:

```yaml
steps:
    plugins:
      - ca-johnson/perforce:
          p4port: my-perforce-server:1666
          p4user: my-username
```

Custom workspace view:

```yaml
steps:
    plugins:
      - ca-johnson/perforce:
          view: >-
            //dev/project/... project/...
            //dev/vendor/... vendor/...
```

Workspace view via a p4 stream:

```yaml
steps:
    plugins:
      - ca-johnson/perforce:
          stream: //dev/minimal
```

## Contributing

1. Install python/requirements.txt
2. Make sure `p4d` is in your `PATH`
3. Make sure your version of `bk` supports `bk local run`

Making changes to `python/`
* Write unit tests
* Implement new functionality
* Iterate via python unit tests

Making changes to `hooks/` and scripts called by hooks
* Add entries to local-pipeline.yml to test new behaviour, if relevant.
* `make` to start p4d on localhost:1666, vendor the plugin, run the pipeline and kill p4d.
