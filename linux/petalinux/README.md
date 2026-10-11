### What is this?
This is a modified version of PetaLinux Yocto project, converted from the original ALINX project for PetaLinux v2020.1 to work with PetaLinux v2022.2.  
There are some problems with SD card negotiation steps during boot up in PetaLinux v2022.2, so some tricks are necessary to make it work. The u-boot script has been modified for this (project-spec/meta-user/recipes-bsp/u-boot/u-boot-zynq-scr/boot.cmd.default.initrd and project-spec/configs/config).  
  
Key changes:  
1. Yocto/BiteBake syntax has been updated to work with new Yocto build engine.
2. SD card negotiation problems are fixed on PetaLinux v2022.2

### Build and package PetaLinux
```
cd ./AXU9EG_AXU15EG/linux/petalinux
petalinux-config --get-hw-description=<path of .xsa file> --silentconfig
petalinux-build
petalinux-package --boot --u-boot --fpga --force
```

### Prepare SD card
Copy build results (images/linux) to SD card first partition (FAT32).
- BOOT.BIN
- boot.scr
- system.dtb
- Image (not image.ub)

### (Optional) Create .wic package
```
petalinux-package --wic --bootfiles "BOOT.BIN boot.scr Image system.dtb"
gzip -f images/linux/petalinux-sdimage.wic
```
The wic.gz image can be used directly to write to SD card using balenaEtcher (https://etcher.balena.io/).

### (Optional) Use pre-downloaded Yocto mirror and sstate cache
You can download Yocto mirror data and sstate cache from Xilinx Petalinux Download page to avoid online downloading and save build time.  
Related configurations are here:
```
vi project-spec/meta-user/conf/petalinuxbsp.conf
```
The lines below are related to Yocto mirror and sstate cache locations. Refer to the location and place the pre-downloaded data there.
```
DL_DIR = "/home/vivado/yocto_mirror"
SSTATE_DIR = "/home/vivado/yocto_sstate_aarch64"
```
### Cautions
Because some tricks are hard-coded, using petalinux-config may have no effect. Please refer to Yocto config file (project-spec/configs/config) and u-boot script (project-spec/meta-user/recipes-bsp/u-boot/u-boot-zynq-scr/boot.cmd.default.initrd).
- bootargs
- Addresses of image loaded
- SD card related settings
