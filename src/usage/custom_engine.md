# Custom container engine

You can use a different container engine that is compatible with
the Docker Engine API, by setting the `DOCKER_HOST` environment variable
to a custom socket path.

## Example how to use `podman` with `actoo` using `sh` shell

```shell
DOCKER_HOST='unix:///var/run/podman/podman.sock' actoo # ...
```

or

```shell
export DOCKER_HOST='unix:///var/run/podman/podman.sock'
actoo # ...
```

## Using `actoo` with remote Docker engine via SSH

```shell
DOCKER_HOST='ssh://user@host' actoo # ...
```

## Using `actoo` with remote Docker engine via SSH in PowerShell

```powershell
$env:DOCKER_HOST = 'ssh://user@host'
actoo # ...
```
