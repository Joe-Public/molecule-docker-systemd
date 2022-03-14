# Fedora latest stable image with systemd enabled

You can use this image as a base container to run systemd services inside.

## Supported tags
 - `latest`, `35`
 - `34`

## Usage

Run the container as a daemon

`docker run -d --privileged --name molecule-fedora -v /sys/fs/cgroup:/sys/fs/cgroup:ro joepublic/molecule-fedora:latest`

Enter to the container

`docker exec -it molecule-fedora bash`
