### Build and package PetaLinux
```
cd ./AXU9EG_AXU15EG/linux/petalinux
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

### (Optional) Create .wic package
```
petalinux-package --wic --bootfiles "BOOT.BIN boot.scr Image system.dtb" \
&& gzip -f images/linux/petalinux-sdimage.wic
```

### Check pre-downloaded Yocto mirror and sstate cache
```
vi project-spec/meta-user/conf/petalinuxbsp.conf
```
The lines below are related to Yocto mirror and sstate cache locations. Refer to the location and place the pre-downloaded data there.
```
DL_DIR = "/home/vivado/yocto_mirror"
SSTATE_DIR = "/home/vivado/yocto_sstate_aarch64"
```
