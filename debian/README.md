# Debian image with systemd enabled

You can use this image as a base container to run systemd services inside.

## Supported tags
 - `latest`, `12`
 - `11`
 - `10`

## Usage

### Test it on the console

First you should start the container as a daemon. For Debain 10 (Buster) and Debian 11 (Bullseye) you have to add `--cgroupns=host` to the command. Starting from Debian 12 (Bookworm) this seems not to be necessary.

Debian 10:

`docker run -d --privileged --name molecule-debian --cgroupns=host -v /sys/fs/cgroup:/sys/fs/cgroup:rw joepublic/molecule-debian:10`

Debian 11:

`docker run -d --privileged --name molecule-debian --cgroupns=host -v /sys/fs/cgroup:/sys/fs/cgroup:rw joepublic/molecule-debian:11`

Debian 12:

`docker run -d --privileged --name molecule-debian -v /sys/fs/cgroup:/sys/fs/cgroup:rw joepublic/molecule-debian:12`

Now you can enter the container and run `systemctl`:

`docker exec -it molecule-debian systemctl`
```
UNIT                              LOAD   ACTIVE     SUB       DESCRIPTION
dev-vda1.device                   loaded activating tentative /dev/vda1
-.mount                           loaded active     mounted   /
dev-hugepages.mount               loaded active     mounted   Huge Pages File System
dev-mqueue.mount                  loaded active     mounted   POSIX Message Queue File System
etc-hostname.mount                loaded active     mounted   /etc/hostname
etc-hosts.mount                   loaded active     mounted   /etc/hosts
etc-resolv.conf.mount             loaded active     mounted   /etc/resolv.conf
sys-fs-fuse-connections.mount     loaded active     mounted   FUSE Control File System
sys-kernel-debug.mount            loaded active     mounted   Kernel Debug File System
systemd-ask-password-console.path loaded active     waiting   Dispatch Password Requests to Console Directory Watch
init.scope                        loaded active     running   System and Service Manager
systemd-journal-flush.service     loaded active     exited    Flush Journal to Persistent Storage
systemd-journald.service          loaded active     running   Journal Service
systemd-modules-load.service      loaded active     exited    Load Kernel Modules
systemd-sysctl.service            loaded active     exited    Apply Kernel Variables
systemd-sysusers.service          loaded active     exited    Create System Users
-.slice                           loaded active     active    Root Slice
system.slice                      loaded active     active    System Slice
systemd-journald-audit.socket     loaded active     running   Journal Audit Socket
systemd-journald-dev-log.socket   loaded active     running   Journal Socket (/dev/log)
systemd-journald.socket           loaded active     running   Journal Socket
basic.target                      loaded active     active    Basic System
cryptsetup.target                 loaded active     active    Local Encrypted Volumes
graphical.target                  loaded active     active    Graphical Interface
local-fs.target                   loaded active     active    Local File Systems
multi-user.target                 loaded active     active    Multi-User System
paths.target                      loaded active     active    Paths
slices.target                     loaded active     active    Slices
sockets.target                    loaded active     active    Sockets
swap.target                       loaded active     active    Swap
sysinit.target                    loaded active     active    System Initialization
timers.target                     loaded active     active    Timers
systemd-tmpfiles-clean.timer      loaded active     waiting   Daily Cleanup of Temporary Directories

LOAD   = Reflects whether the unit definition was properly loaded.
ACTIVE = The high-level unit activation state, i.e. generalization of SUB.
SUB    = The low-level unit activation state, values depend on unit type.

33 loaded units listed. Pass --all to see loaded but inactive units, too.
To show all installed unit files use 'systemctl list-unit-files'.
```

### Use it with molecule

#### Debian 10

A platform definition in molecule.yml could look like this for Debian 10:

```yaml
platforms:
  - name: debian10
    image: joepublic/molecule-debian:10
    command: /lib/systemd/systemd
    pre_build_image: true
    privileged: true
    cgroupns_mode: host
    volumes:
      - /sys/fs/cgroup:/sys/fs/cgroup:rw
```

#### Debian 11

For Debian 10 the only difference would be the tag for the image:

```yaml
platforms:
  - name: debian11
    image: joepublic/molecule-debian:11
    command: /lib/systemd/systemd
    pre_build_image: true
    privileged: true
    cgroupns_mode: host
    volumes:
      - /sys/fs/cgroup:/sys/fs/cgroup:rw
```

#### Debian 12

Compared to the other versions the configuration `cgroupns_mode: host` is not needed.

```yaml
platforms:
  - name: debian12
    image: joepublic/molecule-debian:12
    command: /lib/systemd/systemd
    pre_build_image: true
    privileged: true
    volumes:
      - /sys/fs/cgroup:/sys/fs/cgroup:rw
```
