# Summary

Vanilla is a single-core operating system for the ARMv7 architecture.

# Building

Build the bootloader by `cd bootloader && make`

Flash the bootloader binary at address 0x00400000

Change the serial port in line 92 in the Makefile

Build and upload the kernel with `cd kernel && make`


## Coming soon

- Safe bootloader w/hash check &check;
- Python kernel programmer &check;
- Basic driver support &check;
- Multiclass scheduler w/FPU support and lazy stacking
- System calls
- Runtime program execution (.elf .bin)
- LCD support with video playback (raw format)
- FAT32 stack
- TCP/IP stack
- Server support

# Bootloader

The software embeds a flash bootloader residing inside flash at address 0x00400000. It can open a serial connection with a host computer in order to download the new kernel. The bootloader will load the kernel image to address 0x00404000. The first page of the image must consist of the kernel header. Therefore the actual application and vector table starts at address 0x00404200. The bootloader is accessed in the following ways

- kernel info struct not matching the bootloader info struct
- kernel image not valid (SHA256 mismatch)
- boot signature at address 0x20400000 says "StayInBootloader"
