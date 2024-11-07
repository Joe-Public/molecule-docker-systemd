# Fedora latest stable image with systemd enabled

You can use this image as a base container to run systemd services inside.

## Supported tags
 - `latest`, `41`
 - `40`
 - `39`

## Usage

### Test it on the console

First you should start the container as a daemon.

Fedora 39:

`docker run -d --privileged --name molecule-fedora --cgroupns=host -v /sys/fs/cgroup:/sys/fs/cgroup:rw joepublic/molecule-fedora:39`

Fedora 40:

`docker run -d --privileged --name molecule-fedora --cgroupns=host -v /sys/fs/cgroup:/sys/fs/cgroup:rw joepublic/molecule-fedora:40`

Fedora 41:

`docker run -d --privileged --name molecule-fedora --cgroupns=host -v /sys/fs/cgroup:/sys/fs/cgroup:rw joepublic/molecule-fedora:41`

Now you can enter the container and run `systemctl`:

`docker exec -it molecule-fedora systemctl`
```
  UNIT                            LOAD   ACTIVE     SUB       DESCRIPTION
  dev-vda1.device                 loaded activating tentative /dev/vda1
  -.mount                         loaded active     mounted   Root Mount
  dev-mqueue.mount                loaded active     mounted   POSIX Message Queue File System
  etc-hostname.mount              loaded active     mounted   /etc/hostname
  etc-hosts.mount                 loaded active     mounted   /etc/hosts
  etc-resolv.conf.mount           loaded active     mounted   /etc/resolv.conf
  tmp.mount                       loaded active     mounted   Temporary Directory /tmp
  init.scope                      loaded active     running   System and Service Manager
  systemd-journald.service        loaded active     running   Journal Service
  systemd-tmpfiles-setup.service  loaded active     exited    Create Volatile Files and Directories
  -.slice                         loaded active     active    Root Slice
  system.slice                    loaded active     active    System Slice
  systemd-journald-audit.socket   loaded active     running   Journal Audit Socket
  systemd-journald-dev-log.socket loaded active     running   Journal Socket (/dev/log)
  systemd-journald.socket         loaded active     running   Journal Socket
  basic.target                    loaded active     active    Basic System
  graphical.target                loaded active     active    Graphical Interface
  local-fs.target                 loaded active     active    Local File Systems
  multi-user.target               loaded active     active    Multi-User System
  paths.target                    loaded active     active    Path Units
  slices.target                   loaded active     active    Slice Units
  sockets.target                  loaded active     active    Socket Units
  swap.target                     loaded active     active    Swaps
  sysinit.target                  loaded active     active    System Initialization
  timers.target                   loaded active     active    Timer Units
  systemd-tmpfiles-clean.timer    loaded active     waiting   Daily Cleanup of Temporary Directories

LOAD   = Reflects whether the unit definition was properly loaded.
ACTIVE = The high-level unit activation state, i.e. generalization of SUB.
SUB    = The low-level unit activation state, values depend on unit type.
26 loaded units listed. Pass --all to see loaded but inactive units, too.
To show all installed unit files use 'systemctl list-unit-files'.
```

### Use it with molecule

#### Fedora 39

For Fedora 39 the only difference would be the tag for the image:

```yaml
platforms:
  - name: fedora39
    image: joepublic/molecule-fedora:39
    command: /usr/sbin/init
    pre_build_image: true
    privileged: true
    cgroupns_mode: host
    volumes:
      - /sys/fs/cgroup:/sys/fs/cgroup:rw
```

#### Fedora 40

For Fedora 40 the only difference would be the tag for the image:

```yaml
platforms:
  - name: fedora40
    image: joepublic/molecule-fedora:40
    command: /usr/sbin/init
    pre_build_image: true
    privileged: true
    cgroupns_mode: host
    volumes:
      - /sys/fs/cgroup:/sys/fs/cgroup:rw
```

#### Fedora 41

For Fedora 41 the only difference would be the tag for the image:

```yaml
platforms:
  - name: fedora41
    image: joepublic/molecule-fedora:41
    command: /usr/sbin/init
    pre_build_image: true
    privileged: true
    cgroupns_mode: host
    volumes:
      - /sys/fs/cgroup:/sys/fs/cgroup:rw
```
