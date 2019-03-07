# Software Design Flow
----------------------

This section shows how to generate BOOT.BIN using the PetaLinux build tool and the Xilinx® OpenCV
library.

## PetaLinux Design Flow
### Install PetaLinux
Install PetaLinux as described in the PetaLinux Tools Documentation Reference Guide (UG1144).
### Set PetaLinux Variable
Set the following PetaLinux environment variable $PETALINUX:
% source <path/to/petalinux-installer>/Petalinux-v2018.2/petalinux-v2018.2-final/settings.sh
% echo $PETALINUX


### Build the PetaLinux Project
Use the following commands to create the PetaLinux project:

```bash
cd $TRD_HOME/apu/dpu_petalinux_bsp
petalinux -create -t project -s Xilinx-dpu-trd-zcu102-v2018.2.bsp
cd zcu102-dpu-trd-v2018-2
petalinux -config –get-hw-description=$TRD_HOME/p1/pre-build
petalinux-build
```

### Create BOOT.BIN
Create the boot.bin file:

```bash
cd images/linux
petalinux-package --boot --fsbl zynqmp_fsbl.elf --u-boot u-boot.elf --pmufw pmufw.elf --fpga system.bit
```

