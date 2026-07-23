# pkg-urm

This is the debian packaging side of the userspace-resource-manager project. Upstream project is hosted here: https://github.com/qualcomm/userspace-resource-manager

## Branches

- qli-cli
- qli-staging/debian/latest
- qli-staging/debian/trixie
- qcom/ubuntu/resolute

## Build Instructions

### URM Build Dependencies
```bash
sudo apt-get install -y cmake pkg-config libyaml-dev libsystemd-dev
# Optional packages
sudo apt-get install -y fasttext libfasttext-dev
```

### Install sbuild tool
```bash
sudo apt-get update
sudo apt-get install -y sbuild schroot debootstrap eatmydata ccache
```
 
### Add user to sbuild group
```bash
sudo adduser $USER sbuild
newgrp sbuild
```

### Create an Ubuntu noble chroot
```bash
sudo sbuild-createchroot \
   --include=eatmydata,ccache \
   --components=main,universe \
   noble \
   /srv/chroot/noble-amd64 \
   http://archive.ubuntu.com/ubuntu
```

### Build URM
```bash
cd pkg-urm/
sbuild -d noble
```

### Verify
```bash
ls ../*.deb
```

### Installation Instructions
```bash
sudo dpkg -i ../userspace-resource-manager_1.0.0_amd64.deb
```

### Verify URM service status
```bash
root@debian:/# systemctl status urm
● urm.service - URM Service
     Loaded: loaded (/usr/lib/systemd/system/urm.service; enabled; preset: enabled)
     Active: active (running) since Wed 2026-04-29 18:23:31 UTC; 2s ago
 Invocation: d89c9601c3024687a1db9c63a84d54bf
    Process: 1367 ExecStartPre=/etc/urm/initscripts/post_boot/post_boot.sh (code=exited, status=203/EXEC)
   Main PID: 1368 (urm)
      Tasks: 18 (limit: 37921)
     Memory: 4.7M (peak: 4.7M)
        CPU: 30ms
     CGroup: /urm.slice/urm.service
             └─1368 /usr/bin/urm
```

## Getting in Contact
For support or inquiries, contact: Maintainers.pkg-urm <maintainers.pkg-urm@qualcomm.com>

## Development
We welcome contributions! Please see our CONTRIBUTING.md file for guidelines.

## License
pkg-urm is licensed under the [BSD-3-Clause License](https://spdx.org/licenses/BSD-3-Clause.html). See [LICENSE.txt](LICENSE.txt) for the full license text.
