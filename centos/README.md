# CentOS image with systemd enabled

You can use this image as a base container to run systemd services inside.

## Supported tags
 - `latest`, `8`
 - `7`

## Usage

Run the container as a daemon

`docker run -d --privileged --name molecule-centos -v /sys/fs/cgroup:/sys/fs/cgroup:ro joepublic/molecule-centos:latest`

Enter to the container

`docker exec -it molecule-centos bash`
