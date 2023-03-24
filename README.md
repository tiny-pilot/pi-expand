# pi-expand

[![License](http://img.shields.io/:license-mit-blue.svg?style=flat-square)](LICENSE)
[![CircleCI](https://circleci.com/gh/tiny-pilot/pi-expand.svg?style=svg)](https://circleci.com/gh/tiny-pilot/pi-expand)

## Overview

Expands a Raspberry Pi microSD image to match the disk size.

## Why?

The standard Raspberry Pi microSD image initially writes to a small portion of the microSD. On the microSD's first boot, it expands the filesystem to occupy the full size of the microSD image. If the user cuts power to their device during the expansion, it will corrupt the filesystem, leaving the device in an unbootable state.

If you know the target microSD size in advance, you can perform the expansion step at image creation time, reducing your image's time to first boot and reducing the risk of filesystem corruption.

## Usage

Expand the standard Raspberry Pi OS Lite image to 29800 MiB to fit a 32 GB microSD card:

```bash
sudo ./pi-expand \
  --in 2023-02-21-raspios-bullseye-armhf-lite.img \
  --out 2023-02-21-raspios-bullseye-armhf-lite-expanded.img \
  --size 29800
```

## Tips

* Balena Etcher recognizes unused space in a disk image and can optimize it out of disk writes. Writing an expanded image with Balena Etcher takes approximately the same time as
  * Note that Balena's optimization fails if the image is compressed.
* If you're transferring the image across the network, gzipping it first will reduce file size by an order of magnitude.
