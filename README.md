# Polaris Docker

This container packages [Polaris](https://github.com/agersant/polaris) under [Alpine Linux][https://alpinelinux.org/], a lightweight Linux distribution.

[Published images on Docker Hub](https://hub.docker.com/r/agersant/polaris)

Legacy images can be found on [Quay](https://quay.io/repository/connectical/polaris?tab=tags) and [Gitlab](https://gitlab.com/connectical/container/polaris/container_registry/6397161).

## Run

To run this container:

```sh
docker run -t -d --name=polaris -p 5050:5050 agersant/polaris
```

This start `polaris` and publish the port to host. You can go to http://localhost:5050 to see it running.

⚠️ Warning: this is a basic run, all data will be destroyed after container stop and rm.

## Volumes

This container exports three volumes:

- /music: music files storage directory
- /var/cache/polaris: polaris cache directory
- /var/lib/polaris: polaris data directory

You can exec the following to mount your music dir, cache and data.

```sh
docker run -t -d \
  --name=polaris \
  -p 5050:5050 \
  -v /my/music/directory:/music \
  -v /my/polaris/cache:/var/cache/polaris \
  -v /my/polaris/data:/var/lib/polaris \
  agersant/polaris
```

Take note that you must create before the cache directory `/my/polaris/cache` and data directory `/my/polaris/data` and set ownership to UID/GID 100 in both, otherwise the main proccess will crash.

```sh
mkdir -p /my/polaris/cache /my/polaris/data
chown -R 100:100 /my/polaris/cache /my/polaris/data
```

## Environment variables

The `run-polaris` command can use the following environment variables.

| Variable | Used for | Default value |
| --- | --- | --- |
| POLARIS_PORT | Define listen port | 5050 |
| POLARIS_CONFIG_FILE | Optional config file location | |
| POLARIS_DATA_DIR | Optional data directory location | /var/lib/polaris |
| POLARIS_CACHE_DIR | Optional cache directory location | /var/cache/polaris |
| POLARIS_LOG_LEVEL | Optional log level (off/error/warn/info/debug/trace) | |
