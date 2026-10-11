### Build and package PetaLinux
```
petalinux-config --get-hw-description=<path of .xsa file>
petalinux-build
petalinux-package --boot --u-boot --fpga --force
```
### Copy images to SD card
Copy build results (images/linux) to SD card first partition (FAT32).
- BOOT.BIN
- boot.scr
- system.dtb
- Image (not image.ub)
