# Rocky Linux image with systemd enabled

You can use this image as a base container to run systemd services inside. It already contains the packages needed to manage it with Ansible. The intention is to use it for testing of Ansible with molecule.

## Supported tags
 - `latest`, `9`
 - `8`

## Usage

### Test it on the console

First you should start the container as a daemon.

Rocky Linux 8:

`docker run -d --privileged --name molecule-rockylinux --cgroupns=host -v /sys/fs/cgroup:/sys/fs/cgroup:rw joepublic/molecule-rockylinux:8`

Rocky Linux 9:

`docker run -d --privileged --name molecule-rockylinux --cgroupns=host -v /sys/fs/cgroup:/sys/fs/cgroup:rw joepublic/molecule-rockylinux:9`

Now you can enter the container and run `systemctl`:

`docker exec -it molecule-rockylinux systemctl`

```
UNIT                            LOAD   ACTIVE SUB       DESCRIPTION
-.mount                         loaded active mounted   Root Mount
dev-mqueue.mount                loaded active mounted   POSIX Message Queue File System
etc-hostname.mount              loaded active mounted   /etc/hostname
etc-hosts.mount                 loaded active mounted   /etc/hosts
etc-resolv.conf.mount           loaded active mounted   /etc/resolv.conf
init.scope                      loaded active running   System and Service Manager
systemd-journald.service        loaded active running   Journal Service
systemd-tmpfiles-setup.service  loaded active exited    Create Volatile Files and Directories
-.slice                         loaded active active    Root Slice
system.slice                    loaded active active    System Slice
dbus.socket                     loaded active listening D-Bus System Message Bus Socket
systemd-coredump.socket         loaded active listening Process Core Dump Socket
systemd-journald-dev-log.socket loaded active running   Journal Socket (/dev/log)
systemd-journald.socket         loaded active running   Journal Socket
basic.target                    loaded active active    Basic System
local-fs.target                 loaded active active    Local File Systems
multi-user.target               loaded active active    Multi-User System
paths.target                    loaded active active    Paths
slices.target                   loaded active active    Slices
sockets.target                  loaded active active    Sockets
swap.target                     loaded active active    Swap
sysinit.target                  loaded active active    System Initialization
timers.target                   loaded active active    Timers
systemd-tmpfiles-clean.timer    loaded active waiting   Daily Cleanup of Temporary Directories

LOAD   = Reflects whether the unit definition was properly loaded.
ACTIVE = The high-level unit activation state, i.e. generalization of SUB.
SUB    = The low-level unit activation state, values depend on unit type.

24 loaded units listed. Pass --all to see loaded but inactive units, too.
To show all installed unit files use 'systemctl list-unit-files'.
```

### Use it with molecule

#### Rocky Linux 8

A platform definition in molecule.yml could look like this for Rocky Linux 8:

```yaml
platforms:
  - name: rockylinux8
    image: joepublic/molecule-rockylinux:8
    command: /lib/systemd/systemd
    pre_build_image: true
    privileged: true
    cgroupns_mode: host
    volumes:
      - /sys/fs/cgroup:/sys/fs/cgroup:rw
```

#### Rocky Linux 9

For Rocky Linux 9 the only difference would be the tag for the image:

```yaml
platforms:
  - name: rockylinux9
    image: joepublic/molecule-rockylinux:9
    command: /lib/systemd/systemd
    pre_build_image: true
    privileged: true
    cgroupns_mode: host
    volumes:
      - /sys/fs/cgroup:/sys/fs/cgroup:rw
```
