This is the buildroot board support for the Avnet Zedboard. The Zedboard is
a development board based on the Xilinx Zynq-7000 based All-Programmable
System-On-Chip.

Zedboard information including schematics, reference designs, and manuals are
available from http://www.zedboard.org .

The firmware releases for the Xilinx Zynq silicons depend on Xilinx some propietary tools or code. This dependency has been reduced to a pair of source files available in the regular Xilinx SDK.

You will need this files from Xilinx tree to generate the later listed files:
	ps7_init.c
	ps7_init.h

You will need the following files from output/images:
	zynq-zed.dtb
	rootfs.cpio.uboot
	uImage
	u-boot.img
	boot.bin


uboot.bin  -- U-Boot SPL Support
--------------------------------

Due to licensing issues, the files ps7_init.c/h are not able to be
distributed with the U-Boot source code.  These files are required to make a
boot.bin file.

If you already have the Xilinx tools installed, the following sequence will
unpack, patch and build the rfs, kernel, uboot, and uboot-spl.

make zedboard_defconfig
make uboot-patch
cp ${XILINX}/ISE_DS/EDK/sw/lib/hwplatform_templates/zed_hw_platform/ps7_init.{c,h} \
output/build/uboot-xilinx-v2014.1/board/xilinx/zynq/

Now that you patched the uboot files, you will be capable of compiling the
buildroot.

make


Resulting system
----------------
The SD card should be filled like the following, in a FAT32 partition at the
beggining of the device:
	/boot.bin
	/devicetree.dtb
	/uImage
	/uramdisk.image.gz
	/u-boot.img


All needed files can be taken from output/images/

boot.bin, uImage and u-boot.img are direct copies of the same files
available on output/images/

devicetree.dtb is just zynq-zed.dtb renamed.

uramdisk.image.gz is rootfs.cpio.uboot renamed
