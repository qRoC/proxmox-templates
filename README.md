# Proxmox LXC templates

## Install

### Install DAB

```
$ apt-get install dab
```

### Open template directory(`debian-8.5-minimal-64` for sample) and build

```
$ cd proxmox-templates/debian-8.5-minimal-64
$ make
$ make clean
$ mv debian-8.0-minimal_8.5-1_amd64.tar.gz /var/lib/vz/template/cache/
```

# Notes

  - `PermitRootLogin yes` in `/etc/ssh/sshd_config` not safe.