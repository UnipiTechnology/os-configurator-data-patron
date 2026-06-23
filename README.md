# Os-configurator-data for Unipi Patron

- Unipi Patron specific data for unipi-os-configurator.
- Contains device tree overlays an udev rules for various Unipi Patron models.
- Package name is unipi-os-configurator-data (without the "-patron"!).

## Building

Building requires having the kernel headers.

### Building on Zulu based platform

Install unipi-kernel-headers package.

```sh
make all
make install
```

### Building on non-arm64 architecture

- prepare Zulu kernel building environment in directory ./unipi-kernel

```sh
git clone https://github.com/UnipiTechnology/unipi-kernel.git
cd unipi-kernel
./prepare.sh build
CROSS_COMPILE=aarch64-linux-gnu- ARCH=arm64 make unipi-zulu_defconfig
CROSS_COMPILE=aarch64-linux-gnu- ARCH=arm64 make prepare
cp dts/unipi-zulu.dtsi ../dts
cd ..
```

- build device tree and overlays

```sh
CROSS_COMPILE=aarch64-linux-gnu- ARCH=arm64 make LINUX_BUILD_PATH=$(pwd)/unipi-kernel/linux-imx all
```

- install files to directory ./install

```sh
CROSS_COMPILE=aarch64-linux-gnu- ARCH=arm64 make DESTDIR=$(pwd)/install install
```
