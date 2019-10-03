WHAT IS THIS?
=============

Linux Kernel source code for the devices:
* bq aquaris X5 Plus


BUILD INSTRUCTIONS?
===================

Specific sources are separated by releases with it's corresponding number. First, you should
clone the project:

        $ git clone https://github.com/bq/aquaris-X5-plus.git 

After it, choose the release you would like to build:

*Aquaris X5 Plus*

        $ mv aquaris-X5-plus kernel
        $ cd kernel
        $ git checkout tags/{release}

At the same level of the "kernel" directory:

Download a prebuilt gcc

        $ git clone https://android.googlesource.com/platform/prebuilts/gcc/linux-x86/arm/arm-eabi-4.8

Create KERNEL_OUT dir:

        $ mkdir KERNEL_OUT 
  
Your directory tree should look like this:
* kernel
* arm-eabi-4.8
* KERNEL_OUT

Finally, build the kernel according the next table of product names:

| device                    | product                 |
| --------------------------|-------------------------|
| bq aquaris X5 Plus        | gohan                   |


        make -C android_kernel_bq_msm8976 O=../KERNEL_OUT  ARCH=arm CROSS_COMPILE=../arm-eabi-4.8/bin/arm-eabi- gohan_defconfig
        make O=../KERNEL_OUT/ -C android_kernel_bq_msm8976 ARCH=arm  CROSS_COMPILE=../arm-eabi-4.8/bin/arm-eabi-                       
    
You can specify "-j CORES" argument to speed-up your compilation, example:

        make O=../KERNEL_OUT/ -C android_kernel_bq_msm8976 ARCH=arm  CROSS_COMPILE=../arm-eabi-4.8/bin/arm-eabi- -j 8
        
        
        abootimg --create ./KernelImage/Boot85.img -f ./KernelImage/bootimg.cfg -k ./KERNEL_OUT/arch/arm/boot/zImage-dtb -r ./KernelImage/initrd.img

