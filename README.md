#### SDBox-Multiboot README ####

Boot Workbench from SD card on any Amiga with SDBox!


# HOW TO PREPARE THIS DISK (Read this first!) 

This disk requires workbench files in order to function. 
The files are not included for copyright reasons and must be copied from a Workbench 1.3 floppy as below: 

1. Boot into workbench
2. Insert this disk and run activate-disk
3. Follow the prompts to copy the Workbench files to this disk


Note for SDbox V2 Users

V2 of the SDBox requires a different driver (spisd.device)
The driver is included in the Storage drawer and must be copiied to both DEVS: and Payload/common/devs
The DirWork (DW) file manager is included for this and all your file management needs. 


ABOUT SDBox Multiboot

The purpose of this floppy disk is to boot a Workbench environment compatible with 
the installed kickstart from a connected SDBox device. 

This brings a portable "HDD-like" Workbench environment to any Amiga. 

It's also a general-purpose SDBox utility disk. 

Features:

* Searches SD card for most compatible workbench environment
* Optional RAD: (BOOTRAD) device to reboot from SDBox without a floppy
* Basic SDBox driver install script for internal hard drive
* Can boot Workbench from floppy with SDBox mounted 

Some use cases:

* Turn ANY Amiga into a HDD system! (kinda)
* Data transfer to/from internal fixed storage 
* Recovery of a faulted system
* Use as your daily driver, if you dare
* Mount SDBox then boot Workbench floppy for installation to SD card

DISCLAIMER 

I'm not an Amiga expert. Use entirely at your own risk.

REQUIREMENTS

* Any Amiga with Kickstart 1.3 or higher
* SDBox and micro SD card (see below)
* This floppy
* Workbench 1.3 (some files are required by SDBox Multiboot)


HOW IT WORKS

SDBox Multiboot boot sequence:

1. Copies boot files to RAM: (default) or RAD: (if enabled) and continues boot from there.
2. Mounts the SDBox (device SD0:) 
3. Checks the kickstart version 
4. Looks for a workbench installation at these paths:

    SD0:
    SD0:Workbench
    SD0:SYS
    SD0:BOOTENV/$version/OS (where $version is 13, 204, 31, 32 etc.)

5. Assigns SYS:, DEVS:, LIBS: etc.   
6. Executes startup-sd if present (for shared application assigns)
7. Passes execution to SYS:s/startup-sequence.

The floppy can then be ejected as Workbench will run from the SD card.


HOW TO PREPARE THE MICRO SD CARD

1) MS-DOS partition table
2) A single <4GB Primary Fat32 partition (smaller partitions mount more quickly)


INSTALLING WORKBENCH TO SD0: FROM AMIGA

1) Insert the prepared SD card into SDBOX and boot from this floppy
2) When prompted, insert your Workbench or WB Install floppy to DF0: and hit enter
3) Once booted, install Workbench to SD0: in the usual way


INSTALLING MULTIPLE WORKBENCHES FROM PC

1) Create the below drawers as required:

   BOOTENV/13/OS
   BOOTENV/204/OS
   BOOTENV/31/OS
   BOOTENV/314/OS
   BOOTENV/32/OS
   BOOTENV/321/OS
   BOOTENV/322/OS

2) Dump Workbench floppies OR copy HDD installations to the appropriate OS drawers. 

Alternatively if you only want to run a single workbench it can be copied to 
the root of the SD card.

Install the micro SD card and enjoy!
 
 
USING BOOTRAD (Persistent boot)

When BOOTRAD is enabled the boot files will be copied to recoverable RAMDrive 
("BOOTRAD") instead of RAM. Workbench can then be rebooted from the SDBox without using this disk.

To Enable BOOTRAD

1) From workbench, open SDBox Multiboot and run enable-bootrad
2) BOOTRAD is enabled at next floppy boot 

To Disable BOOTRAD

1) From Workbench, open SD Multiboot and run disable-bootrad

Active BOOTRAD can also be cleared by powering-off the Amiga. 

CAVEATS:
BOOTRAD will occupy a chunk of chipram as long as it is active, whereas 
booting from RAM: (default) releases used memory after boot completes.

BOOTRAD consumes more memory on Kickstart 1.3 systems as DOS commands must also be stored. 
On 2.0+ systems BOOTRAD can be smaller as more DOS commands are in ROM.

As such BOOTRAD is not recommended on stock 1.3 Amigas. 


OTHER NOTES

RAD size could likely be optimised a little more by reducing sector size on >2.0 systems
but this does not appear to be possible (mount fails when SectorSize = 256). 

Another option to reduce RAD size could be a compressed boot image that unpacks to RAM
at boot time but LhA executable is already as large as current RAD. 





