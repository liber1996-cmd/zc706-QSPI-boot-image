# zc706-QSPI-boot-image
How to boot QSPI images on a ZCU706 board using U-Boot distro boot

## **DESCRIPTION**
This Answer Record describes how to boot QSPI images on a ZCU706 board using U-Boot distro boot in 2021.1 of PetaLinux.

## **SOLUTION**
1. Create a PetaLinux project for a ZCU706 board using a template or BSP.

``` 
$ petalinux-create -t project -s <path_to_bsp>/xilinx-zc706-v2021.1-final.bsp
$ cd xilinx-zc706-2021.1

```
2. Configure the project with a QSPI partition.

If you cannot know the memory allocation in advance, you need to run the following command first, and allocate the flash space yourself according to the size of the project file of the build.

