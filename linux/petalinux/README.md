### Build PetaLinux
petalinux-config --get-hw-description=<path of .xsa file>
petalinux-build
petalinux-package --boot --u-boot --fpga --force

Copy images/linux/BOOT.BIN, boot.scr, system.dtb, Image to SD card first partition (FAT32).
