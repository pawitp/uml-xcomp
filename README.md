User Mode Linux (UML) with CyanogenMod's TRANSPARENT_COMPRESSION support. Allows you to mount CyanogenMod file system images with compressed files.

How to use
==========
* Run the it with
    - `./linux ubda=rootfs.ext2`
* Login with username "root" and no password
* Mount host file system with
    - `mkdir /host`
	- `mount -t hostfs none /host`
* Now the filesystem of your host system is available at /host. Mount your desired ext4 image with
    - `mount -t ext4 -o loop /host/path/to/system.img /mnt`
* Modify or extract what you want in /mnt. Note that you must modify it within UML.
* Unmount
    - `umount /mnt`
* Close UML
    - `halt`

Sources
=======

Kernel
------
Kernel from https://cdn.kernel.org/pub/linux/kernel/v3.x/linux-3.10.93.tar.xz

Applied following patches (they should apply cleanly):

    https://github.com/CyanogenMod/android_kernel_cyanogen_msm8916/commit/f73d668898e5996ea7a985b4661e8648716e1fe8.patch
	https://github.com/CyanogenMod/android_kernel_cyanogen_msm8916/commit/d54ef65eda0923f7567ee1effde28bc24e38e501.patch
	https://github.com/CyanogenMod/android_kernel_cyanogen_msm8916/commit/f86d62e96d862a0999016e1213a7f4f3a611e9c9.patch
	https://github.com/CyanogenMod/android_kernel_cyanogen_msm8916/commit/3b432932e3e1ffad2980ee53fe286cbf887fa81f.patch
	https://github.com/CyanogenMod/android_kernel_cyanogen_msm8916/commit/afb22f6262df1a39c2ef52646839502d61220ffb.patch
	https://github.com/CyanogenMod/android_kernel_cyanogen_msm8916/commit/ad1310c997bda926a66afc2787227a95cd8909f3.patch
	https://github.com/CyanogenMod/android_kernel_cyanogen_msm8916/commit/70d3b57af683ce51642123509d9d0a9c7459ee03.patch
	https://github.com/CyanogenMod/android_kernel_cyanogen_msm8916/commit/48886e1e90dbe348c45989d5eead9f7b6c740f57.patch
	https://github.com/CyanogenMod/android_kernel_cyanogen_msm8916/commit/559d826ab6703c48708b5146d45fcc9c666e04fd.patch
	https://github.com/CyanogenMod/android_kernel_cyanogen_msm8916/commit/321fc8332dccc80c9ecd01a0fb68c483c2dbac80.patch
	https://github.com/CyanogenMod/android_kernel_cyanogen_msm8916/commit/3ec68c7e54e1b45d57c5a4b5fd02e4e25380e398.patch

Built with:

	export ARCH=um
	make defconfig
	make menuconfig # Enable File systems -> Transparent compression and Device Drivers -> Block devices -> Loopback device support
	make
	strip linux

Rootfs
------
Built using buildroot from http://buildroot.uclibc.org/downloads/buildroot-2015.11.tar.gz

Built with:

	make defconfig
	make menuconfig # Set Toolchain -> Toolchain type -> External toolchain, enable Filesystem images -> ext2/3/4 root filesystem
	make # Result in output/images
