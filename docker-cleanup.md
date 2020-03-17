# Prune unused Docker objects
## Prune images

The `docker image prune` command allows you to clean up unused images. By default, `docker image prune` only cleans up dangling images. A dangling image is one that is not tagged and is not referenced by any container. To remove dangling images:

```bash
$ docker image prune

WARNING! This will remove all dangling images.
Are you sure you want to continue? [y/N] y
```

To remove all images which are not used by existing containers, use the -a flag:
```bash
$ docker image prune -a

WARNING! This will remove all images without at least one container associated to them.
Are you sure you want to continue? [y/N] y
```

## Prune containers

When you stop a container, it is not automatically removed unless you started it with the --rm flag. To see all containers on the Docker host, including stopped containers, use `docker ps -a`. You may be surprised how many containers exist, especially on a development system! A stopped container’s writable layers still take up disk space. To clean this up, you can use the docker container prune command.
```bash
$ docker container prune

WARNING! This will remove all stopped containers.
Are you sure you want to continue? [y/N] y
```
## Prune volumes

Volumes can be used by one or more containers, and take up space on the Docker host. Volumes are never removed automatically, because to do so could destroy data.
```bash
$ docker volume prune

WARNING! This will remove all volumes not used by at least one container.
Are you sure you want to continue? [y/N] y
```

## Prune networks

Docker networks don’t take up much disk space, but they do create iptables rules, bridge network devices, and routing table entries. To clean these things up, you can use docker network prune to clean up networks which aren’t used by any containers.
```bash
$ docker network prune

WARNING! This will remove all networks not used by at least one container.
Are you sure you want to continue? [y/N] y
```

## Prune everything

The docker system prune command is a shortcut that prunes images, containers, and networks. In Docker 17.06.0 and earlier, volumes are also pruned. In Docker 17.06.1 and higher, you must specify the `--volumes` flag for docker system prune to prune volumes.
```bash
$ docker system prune

WARNING! This will remove:
        - all stopped containers
        - all networks not used by at least one container
        - all dangling images
        - all build cache
Are you sure you want to continue? [y/N] y
```
If you are on Docker 17.06.1 or higher and want to also prune volumes, add the `--volumes` flag:
```bash
$ docker system prune --volumes

WARNING! This will remove:
        - all stopped containers
        - all networks not used by at least one container
        - all volumes not used by at least one container
        - all dangling images
        - all build cache
Are you sure you want to continue? [y/N] y
```


## Link
Based on https://docs.docker.com/config/pruning/
