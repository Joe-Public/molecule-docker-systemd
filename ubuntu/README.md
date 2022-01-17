# Ubuntu image with systemd enabled

You can use this image as a base container to run systemd services inside.

## Supported tags
 - `latest`, `21.10`
 - `21.04`
 - `20.10`
 - `20.04`
 - `18.04`
 - `16.04`

## Usage

Run the container as a daemon

`docker run -d --privileged --name systemd-ubuntu -v /sys/fs/cgroup:/sys/fs/cgroup:ro joepublic/systemd-ubuntu:latest`

Enter to the container

`docker exec -it systemd-ubuntu bash`
