# rtl8812au

Realtek 8812AU/8821AU USB WiFi driver.

for AC1200 (801.11ac) Wireless Dual-Band USB Adapter

This code is base on version 4.3.14 from https://github.com/diederikdehaas/rtl8812AU

### Update for NVidia Jestson Nano support

This code was forked from https://github.com/abperiasamy/rtl8812AU_8821AU_linux

## Known Supported Devices:

```
* COMFAST 1200Mbps USB Wireless Adapter(Model: CF-912AC)
* TP-LINK AC1200 Wireless Dual Band USB Adapter(Model: Archer-T4U)
* TP-LINK AC600 Wireless Dual Band USB Adapter(Model: Archer-T2U Nano)
```

## Compiling with DKMS

```sh
# sudo make -f Makefile.dkms install
```

### Compiling for NVidia Jeston Nano

```sh
# CONFIG_PLATFORM_ARM_JET_NANO = y
```

### Compiling for Raspberry Pi (3)

Install kernel headers and other dependencies.

```sh
# sudo apt-get install linux-image-rpi-rpfv linux-headers-rpi-rpfv raspberrypi-kernel-headers dkms build-essential bc
```

Install kernel headers: https://github.com/notro/rpi-source/wiki

```sh
sudo wget https://raw.githubusercontent.com/notro/rpi-source/master/rpi-source -O /usr/local/bin/rpi-source && sudo chmod +x /usr/local/bin/rpi-source && /usr/local/bin/rpi-source -q --tag-update
rpi-source
```

Edit Makefile and turn on ``CONFIG_PLATFORM_ARM_RPI``, turn off ``CONFIG_PLATFORM_I386_PC``

```sh
CONFIG_PLATFORM_I386_PC = n
CONFIG_PLATFORM_ARM_RPI = y
```

```sh
# cd /usr/src/rtl8812au
# sudo make clean
# sudo make -j4
# sudo make install
# sudo modprobe -a rtl8812au
```

### Compiling for Ubuntu (16.04) and Debian (9)

Download archive into temp directory

```sh
# mkdir -p /tmp/t4u
# cd /tmp/t4u
# wget https://github.com/abperiasamy/rtl8812AU_8821AU_linux/archive/master.zip
```

Unzip

```sh
# unzip master.zip
# cd rtl8812AU_8821AU_linux-master
```
Install kernel headers 

```sh
# sudo apt install linux-headers-$(uname -r)
```

Compile and install from source

```sh
# make
# sudo make install
```

Load module

```sh
# sudo modprobe -a rtl8812au
```

#  Cross-compiling.  You can now specify variables on the command line w/out editing
#  makefile.  For instance, this builds against recent OpenWRT neo2 platform.  Your
#  Cross-compile binaries should be in your PATH.

KSRC=/home/greearb/git/openwrt-neo2-dev/build_dir/target-aarch64_cortex-a53_musl/linux-sunxi_cortexa53/linux-4.14.78 EXT_EXTRA_CFLAGS=-DCONFIG_LITTLE_ENDIAN ARCH=arm64 CROSS_COMPILE=aarch64-openwrt-linux- MODDESTDIR=/tmp make V=1


Setup DKMS

```sh
# sudo apt-get update
# sudo apt-get install dkms
# cd /tmp/t4u/rtl8812AU_8821AU_linux-master/
# sudo cp -R . /usr/src/rtl8812AU_8821AU_linux-1.0
# sudo dkms add -m rtl8812AU_8821AU_linux -v 1.0
# sudo dkms build -m rtl8812AU_8821AU_linux -v 1.0
# sudo dkms install -m rtl8812AU_8821AU_linux -v 1.0
```

## Contributors
<!-- DO NOT EDIT - CONTRIBUTORS.md is autogenerated from git commit log by contributors.sh script. -->

- Anand Babu (AB) Periasamy
- Andreas Hofmann
- Andrew Mann
- AndyPi
- Anton
- archshift
- bits3rpent
- Chen Minqiang
- Daiki Tamada
- Fjodor42
- gremsto
- HackDefendr
- Harshavardhana
- jjones-jr
- Joe
- Joe Acosta
- John Lenz
- Jos Dehaes
- Karl-Philipp Richter
- Marco Milanesi
- Mauro Ribeiro
- Maximilian Schwerin
- mpoly
- Nick Bartos
- Peter H. Li
- pgroenbech
- scrivy
- Taehan Stott
- Vicent Llongo
- Victor Azizi
- 赵迤晨 (Zhao, Yichen)
