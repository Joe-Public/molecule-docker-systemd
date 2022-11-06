# Debian image with systemd enabled

You can use this image as a base container to run systemd services inside.

## Supported tags
 - `testing`, `12`
 - `latest`, `11`
 - `10`

## Usage

Run the container as a daemon

`docker run -d --privileged --name molecule-debian -v /sys/fs/cgroup:/sys/fs/cgroup:ro joepublic/molecule-debian:latest`

Enter to the container

`docker exec -it molecule-debian bash`
