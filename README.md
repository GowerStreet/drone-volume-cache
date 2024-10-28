# drone-volume-cache

This is a pure Bash [Woodpecker CI](https://woodpecker-ci.org/) plugin to cache files and/or folders to a locally mounted volume based on [Drillster/drone-volume-cache](https://github.com/Drillster/drone-volume-cache).

For more information on how to use the plugin, please take a look at [the docs](https://github.com/Gowerstreet/drone-volume-cache/blob/master/DOCS.md).

## Docker
Build and push a new version of the docker image by running:

```bash
docker build --rm=true -t gowerstreet/drone-volume-cache:latest .
docker push gowerstreet/drone-volume-cache:latest
```

## Usage
Execute from the working directory:

```bash
docker run --rm \
  -e PLUGIN_REBUILD=true \
  -e PLUGIN_MOUNT="./node_modules" \
  -e CI_REPO_OWNER="foo" \
  -e CI_REPO_NAME="bar" \
  -e CI_PIPELINE_NUMBER=0 \
  -v $(pwd):$(pwd) \
  -v /tmp/cache:/cache \
  -w $(pwd) \
  gowerstreet/drone-volume-cache
```

Or add in your docker compose file:

```yaml
restore-cache:
  image: gowerstreet/drone-volume-cache
  volumes:
    - "/tmp/cache:/cache"
  settings:
    mount:
      - local-m2
    restore: true
```
