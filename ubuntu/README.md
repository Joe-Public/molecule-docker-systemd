# Ubuntu image with systemd enabled

You can use this image as a base container to run systemd services inside.

## Supported tags
 - `latest`, `22.10`
 - `lts`, `22.04`
 - `20.04`
 - `18.04`
 - `16.04`

## Usage

Run the container as a daemon

`docker run -d --privileged --name molecule-ubuntu -v /sys/fs/cgroup:/sys/fs/cgroup:ro joepublic/molecule-ubuntu:latest`

Enter to the container

`docker exec -it molecule-ubuntu bash`
