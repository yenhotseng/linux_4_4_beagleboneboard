# linux_4_4_beagleboneboard

[Prerequisites]
Develop under ubuntu 18.04(64-bit)

$ sudo apt-get install gcc-arm-linux-gnueabi // ARM Cross Compiler
$ sudo apt-get install git // for "git clone git://github.com/beagleboard/linux.git"


[Ver-4.4 Kernel source]
-- https://github.com/beagleboard/linux/tree/4.4

$ git clone https://github.com/yenhotseng/linux_4_4_beagleboneboard/tree/master/linux

PS: 
$ git clone git://github.com/beagleboard/linux.git
$ cd linux
$ git checkout 4.4

// Modified from VT-Buds /proc/config.gz


$ sudo apt-get install lzop // The Linux Kernel is compressed using lzo. Install the lzop parallel file compressor
$ sudo apt-get install libssl-dev // Building U-Boot requires libssl-dev to be installed

[Build u-boot]
$ cd u-boot

$ make sandbox_defconfig tools-only

$ sudo install tools/mkimage /usr/local/bin

[Compiling the BeagleBone Black Kernel]

Here we compile the BeagleBone Black Kernel, and generate an uImage file with a DTB blob:

$ make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- vt.org_defconfig // put in %kernel%/arch/arm/configs/vt.org_defconfig
$ make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- -j4
$ make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- uImage dtbs LOADADDR=0x80008000 -j4

Now we build any kernel modules:

$ make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- modules -j4

And if you have your rootfs ready, you can install them:

$ make ARCH=arm CROSS_COMPILE=arm-linux-gnueabi- INSTALL_MOD_PATH=/home/cpeacock/export/rootfs modules_install

ref: https://wiki.beyondlogic.org/index.php/BeagleBoneBlack_Building_Kernel

