---
layout: page
title: RedHat & Docker
subtitle: Set up RedHat and Docker
---

# Environment
- RedHat (RHEL 9)
    - yum
- Docker (Mirantis Container Runtime)
- Virtual Box

## RedHat Package
- net-tools
    - `ifconfig` (Check IP Address)

# Linux Commands
- Search for the package which provided the commands / exec
    - `yum provides <Command-Exec>`
- Install package
    - `yum -y install <Package-Name>`
- Check any directory/files owned by unknown user 
    - `find [directory] -nouser -ls`
- Check any directory/files owned by unknown group
    - `find [directory] -nogroup -ls`