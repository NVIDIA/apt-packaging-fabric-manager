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
- [Building Manually](#Building-Manually)
- [Related](#Related)
  * [NSCQ library](#NSCQ-library)
  * [NVIDIA driver](#NVIDIA-driver)
- [See also](#See-also)
  * [RPM](#RPM)
- [Contributing](#Contributing)


## Deliverables

This repo contains the template files used to build the following **DEB** packages:


> _note:_ `XXX` is the first `.` delimited field in the driver version, ex: `460` in `460.32.03`

```shell
- cuda-drivers-fabricmanager
- cuda-drivers-fabricmanager-XXX
- nvidia-fabricmanager-XXX
- nvidia-fabricmanager-dev-XXX

> ex: cuda-drivers-fabricmanager_460.32.03-1_amd64.deb
      cuda-drivers-fabricmanager-460_460.32.03-1_amd64.deb
      nvidia-fabricmanager-460_460.32.03-1_amd64.deb
      nvidia-fabricmanager-dev-460_460.32.03-1_amd64.deb
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

* https://developer.download.nvidia.com/compute/cuda/redist/fabricmanager/

  *ex:* fabricmanager-linux-x86_64-460.32.03.tar.gz

### Install build dependencies
> *note:* these are only needed for building not installation

```shell
# Packaging
apt-get install debhelper devscripts dpkg-dev
```

## Building Manually

### Parse JSON to retrieve download URL
```shell
baseURL="https://developer.download.nvidia.com/compute/cuda/redist"
curl -s $baseURL/redistrib_460.32.03.json | \
jq -r '."fabricmanager" | ."460.32.03" | ."linux-x86_64"' | \
sed "s|^|$baseURL/|"
```

### Create a temp directory
```shell
cd apt-packaging-fabric-manager
mkdir build
rsync -a debian build/
```

### Extract tarball
```shell
tar -C build/ -xf fabricmanager*.tar.gz
cd build
mv fabricmanager/* $PWD
rmdir fabricmanager
```

### Fill variables
```shell
make -f debian/rules fill_templates VERSION=460.32.03 BRANCH=460 DEB_HOST_ARCH=amd64
```
> _note:_ branch is the first `.` delimited field in the driver version, ex: `460` in `460.32.03`

### Generate .deb packages
```shell
DEB_BUILD_OPTIONS=nostrip DEB_HOST_ARCH=amd64 \
dpkg-buildpackage -b
cd ..
ls *.deb
```


## Related

### NSCQ library

- libnvidia-nscq
  * [https://github.com/NVIDIA/apt-packaging-libnvidia-nscq](https://github.com/NVIDIA/apt-packaging-libnvidia-nscq)

### NVIDIA driver

- nvidia-driver
  * [https://github.com/NVIDIA/ubuntu-packaging-nvidia-driver](https://github.com/NVIDIA/ubuntu-packaging-nvidia-driver)


## See also

### RPM

  * [https://github.com/NVIDIA/yum-packaging-fabric-manager](https://github.com/NVIDIA/yum-packaging-fabric-manager)

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md)
