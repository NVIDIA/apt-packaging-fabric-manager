# apt packaging fabric manager

[![License](https://img.shields.io/badge/license-MIT-green.svg)](https://opensource.org/licenses/MIT-license)
[![Contributing](https://img.shields.io/badge/Contributing-Developer%20Certificate%20of%20Origin-violet)](https://developercertificate.org)

## Overview

Packaging templates for `apt` based Linux distros to build NVIDIA fabricmanager packages.

Fabric Manager is intended for hardware containing NvSwitch such as DGX systems.

> _note:_ the version of fabricmanager must match the NVIDIA driver installed.

## Table of Contents

- [Overview](#Overview)
- [Deliverables](#Deliverables)
- [Installation](#Installation)
- [Prerequisites](#Prerequisites)
  * [Clone this git repository](#Clone-this-git-repository)
  * [Install build dependencies](#Install-build-dependencies)
- [Related](#Related)
  * [NSCQ library](#NSCQ-library)
  * [NVIDIA driver](#NVIDIA-driver)
- [Contributing](#Contributing)


## Deliverables

This repo contains the template files used to build the following **DEB** packages:


> _note:_ `XXX` is the first `.` delimited field in the driver version, ex: `460` in `460.32.03`

```shell
- cuda-drivers-fabricmanager
- cuda-drivers-fabricmanager-XXX
- nvidia-fabricmanager-XXX
- nvidia-fabricmanager-dev-XXX
```


## Installation

* **Debian**

  ```shell
  apt-get install cuda-drivers-fabricmanager-XXX
  ```

* **Ubuntu**

  ```shell
  apt-get install cuda-drivers-fabricmanager-XXX
  ```


## Prerequisites

### Clone this git repository:

Supported branches: `main`

```shell
git clone https://github.com/NVIDIA/apt-packaging-fabric-manager
```

### Download a NVIDIA fabricmanager tarball:

* TBD

  *ex:* fabricmanager-460.32.03.tar.gz

### Install build dependencies
> *note:* these are only needed for building not installation

```shell
# Packaging
apt-get install debhelper devscripts dpkg-dev
```

## Related

### NSCQ library

- libnvidia-nscq
  * [https://github.com/NVIDIA/apt-packaging-libnvidia-nscq](https://github.com/NVIDIA/apt-packaging-libnvidia-nscq)

### NVIDIA driver

- nvidia-driver
  * [https://github.com/NVIDIA/ubuntu-packaging-nvidia-driver](https://github.com/NVIDIA/ubuntu-packaging-nvidia-driver)


## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md)
