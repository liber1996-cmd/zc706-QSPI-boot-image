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

`$ petalinux-build`

Use petalinux-config to configure the flash space for each part of the files in images/linux/ in the project just generated.

File correspondence as following:  
The flash memory of the whole zc706 development board is 32MB
- **BOOT.bin** includes：

|Files     |                                                      Size  |
|:---:|:---:|
|zynq_fsbl.elf     |                                                      502KB  |
|Project_1.bit      |                                                     1.7MB  |
|u-boot.elf         |                                                     7.2MB  |
|system.dtb            |                                                  26KB   | 

So we allocate **10MB** to BOOT.bin  

- **bootenv** :no file correspondence but still need the size of **0.2MB**   

- **Image** includes：image.ub                                           **13.25MB**  
- **Rootfs** includes: rootfs.cpio.gz.u-boot                                  **8.25MB**  


|Flash Partition Name|Partion Address|Partition Size|  
|:---:|:---:|:---:|   
|0~0xA00000  |                                 10MB          |                 boot|  
|0xA00000~0xA30000 |                小于0.2MB(0x30000)     |     bootenv|  
|0xA30000~0x1770000  |              13.25MB(0xD40000)  |Image（kernel）|  
|0x1770000~0x 17C0000 |                 大于0.3MB(0x50000)      | bootscr|  
|0x17C0000~ 0x2000000  |             8.25MB(0x840000)    |Rootfs|  

**Attention**： Image is conresponding to kernel in the following image.  















