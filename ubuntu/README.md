# Ubuntu image with systemd enabled

You can use this image as a base container to run systemd services inside.

## Supported tags
 - `latest`, `24.10`
 - `lts`, `24.04`
 - `22.04`
 - `20.04`

## Usage

### Test it on the console

First you should start the container as a daemon.

Ubuntu 20.04:

`docker run -d --privileged --name molecule-ubuntu --cgroupns=host -v /sys/fs/cgroup:/sys/fs/cgroup:rw joepublic/molecule-ubuntu:20.04`

Ubuntu 22.04:

`docker run -d --privileged --name molecule-ubuntu --cgroupns=host -v /sys/fs/cgroup:/sys/fs/cgroup:rw joepublic/molecule-ubuntu:22.04`

Ubuntu 24.04:

`docker run -d --privileged --name molecule-ubuntu --cgroupns=host -v /sys/fs/cgroup:/sys/fs/cgroup:rw joepublic/molecule-ubuntu:24.04`

Ubuntu 24.10:

`docker run -d --privileged --name molecule-ubuntu --cgroupns=host -v /sys/fs/cgroup:/sys/fs/cgroup:rw joepublic/molecule-ubuntu:24.10`

Now you can enter the container and run `systemctl`:

`docker exec -it molecule-ubuntu systemctl`
```
  UNIT                               LOAD   ACTIVE SUB     DESCRIPTION
  -.mount                            loaded active mounted Root Mount
  dev-mqueue.mount                   loaded active mounted POSIX Message Queue File System
  etc-hostname.mount                 loaded active mounted /etc/hostname
  etc-hosts.mount                    loaded active mounted /etc/hosts
  etc-resolv.conf.mount              loaded active mounted /etc/resolv.conf
  init.scope                         loaded active running System and Service Manager
  systemd-journald.service           loaded active running Journal Service
  systemd-remount-fs.service         loaded active exited  Remount Root and Kernel File Systems
  systemd-tmpfiles-setup-dev.service loaded active exited  Create Static Device Nodes in /dev
  systemd-tmpfiles-setup.service     loaded active exited  Create Volatile Files and Directories
  -.slice                            loaded active active  Root Slice
  system.slice                       loaded active active  System Slice
  systemd-journald-audit.socket      loaded active running Journal Audit Socket
  systemd-journald-dev-log.socket    loaded active running Journal Socket (/dev/log)
  systemd-journald.socket            loaded active running Journal Socket
  basic.target                       loaded active active  Basic System
  graphical.target                   loaded active active  Graphical Interface
  local-fs-pre.target                loaded active active  Local File Systems (Pre)
  local-fs.target                    loaded active active  Local File Systems
  multi-user.target                  loaded active active  Multi-User System
  paths.target                       loaded active active  Paths
  slices.target                      loaded active active  Slices
  sockets.target                     loaded active active  Sockets
  swap.target                        loaded active active  Swap
  sysinit.target                     loaded active active  System Initialization
  timers.target                      loaded active active  Timers
  systemd-tmpfiles-clean.timer       loaded active waiting Daily Cleanup of Temporary Directories

LOAD   = Reflects whether the unit definition was properly loaded.
ACTIVE = The high-level unit activation state, i.e. generalization of SUB.
SUB    = The low-level unit activation state, values depend on unit type.

27 loaded units listed. Pass --all to see loaded but inactive units, too.
To show all installed unit files use 'systemctl list-unit-files'.
```

### Use it with molecule

#### Ubuntu 20.04

A platform definition in molecule.yml could look like this for Ubuntu 20.04:

```yaml
platforms:
  - name: ubuntu20_04
    image: joepublic/molecule-ubuntu:20.04
    command: /lib/systemd/systemd
    pre_build_image: true
    privileged: true
    cgroupns_mode: host
    volumes:
      - /sys/fs/cgroup:/sys/fs/cgroup:rw
```

#### Ubuntu 22.04

For Ubuntu 22.04 the only difference would be the tag for the image:

```yaml
platforms:
  - name: ubuntu22_04
    image: joepublic/molecule-ubuntu:22.04
    command: /lib/systemd/systemd
    pre_build_image: true
    privileged: true
    cgroupns_mode: host
    volumes:
      - /sys/fs/cgroup:/sys/fs/cgroup:rw
```

#### Ubuntu 24.04

For Ubuntu 24.04 the only difference would be the tag for the image:

```yaml
platforms:
  - name: ubuntu24_04
    image: joepublic/molecule-ubuntu:24.04
    command: /lib/systemd/systemd
    pre_build_image: true
    privileged: true
    cgroupns_mode: host
    volumes:
      - /sys/fs/cgroup:/sys/fs/cgroup:rw
```

#### Ubuntu 24.10

For Ubuntu 24.10 the only difference would be the tag for the image:

```yaml
platforms:
  - name: ubuntu24_10
    image: joepublic/molecule-ubuntu:24.10
    command: /lib/systemd/systemd
    pre_build_image: true
    privileged: true
    cgroupns_mode: host
    volumes:
      - /sys/fs/cgroup:/sys/fs/cgroup:rw
```
