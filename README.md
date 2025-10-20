# SDBox Multiboot

## INITAL SETUP (Read this before using!) 

This disk requires some files from Workbench 1.3 and the correct drivers for 
your version of SDBox:  

1. Boot into workbench
2. Insert this disk and run Setup
3. Select Import Workbench Files and follow the prompts
4. Select your version of the SDBox (V1 / V2)
5. Enable BOOTRAD if required (persistent boot RAD: device) 


## ABOUT SDBox Multiboot (SDBM)

SDBM is a disk to boot Workbench from a connected SDBox.  

SDBox is cheap, fast, and compatible with all Amigas. Running Workbench 
from SD card via SDBox makes it far more usable on any low-end Amiga. 

It's like having a portable Hard Drive for all your Amigas.

SDBM is also able to select from multiple Workbench installations on an
SD card and boot the one that matches your Kichstart version. 

It's also a general-purpose SDBox driver and utility disk. 


### Features:

* Searches SD card for most compatible workbench environment
* Optional RAD: (BOOTRAD) device to reboot from SDBox without a floppy
* Basic SDBox driver install script for internal hard drive
* Can boot Workbench from floppy with SDBox mounted 


### Some use cases:

* Turn ANY Amiga into a HDD system! (kinda)
* Data transfer to/from internal fixed storage 
* Recovery of a faulted system
* Use as your daily driver, if you dare
* Mount SDBox then boot Workbench floppy for installation to SD card


## DISCLAIMER 

SDBox is not as robust as a conventional HDD system.
It can be picky with SD cards, power sources, and there is no CRC on writes. 
Use is entirely at your own risk! Please see the GitHub page for more info. 


## REQUIREMENTS

* Any Amiga with Kickstart 1.3 or higher
* SDBox and micro SD card (see below)
* This floppy disk
* Workbench 1.3 (some files are required by SDBox Multiboot)


## HOW IT WORKS

### SDBox Multiboot boot sequence:

1. Copies boot files to RAM: (default) or RAD: (if enabled) and continues boot from there.
2. Mounts the SDBox (device SD0:) 
3. Checks the kickstart version 
4. Looks for a workbench installation at these paths:

    SD0:
    SD0:Workbench
    SD0:SYS
    SD0:BOOTENV/$version/OS (where $version is 13, 204, 31, 32 etc.)

5. Assigns SYS:, DEVS:, LIBS: etc.   
6. Executes startup-sd if present 
   (eg. for application assigns shared with multiple workbench instances)
7. Passes execution to SYS:s/startup-sequence.

The floppy can then be ejected as Workbench will run from the SD card.


## HOW TO PREPARE THE MICRO SD CARD

1) Partition with MS-DOS partition table
2) Create a single <4GB Primary Fat32 partition 
   (smaller partitions mount more quickly)


## INSTALLING WORKBENCH TO SD0: FROM AMIGA

1) Insert the prepared SD card into SDBOX and boot from this floppy
2) When prompted, insert your Workbench or WB Install floppy to DF0: and hit enter
3) Once booted, install Workbench to SD0: as if installing to DH0:


## INSTALLING MULTIPLE WORKBENCHES FROM PC

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
 
 
## USING BOOTRAD (Persistent boot)

When BOOTRAD is enabled the boot files will be copied to recoverable RAMDrive 
("BOOTRAD") instead of RAM. Workbench can then be rebooted from the SDBox without using this disk.

To Enable/Disable BOOTRAD

1) From workbench, open SDBox Multiboot and run Setup
2) Toggle BOOTRAD so it shows as enabled or disabled as required
3) The change will take effect on next boot

Active BOOTRAD can also be cleared by powering-off the Amiga. 

CAVEATS:
BOOTRAD will occupy a chunk of chipram as long as it is active, whereas 
booting from RAM: (default) releases used memory after boot completes.

BOOTRAD consumes more memory on Kickstart 1.3 systems as DOS commands must also be stored. 
On 2.0+ systems BOOTRAD can be smaller as more DOS commands are in ROM.

As such BOOTRAD is not recommended on Amigas with <1MB RAM and Kickstart 1.3. 

Also note the Disclaimer above regarding use of the SDBox. 
As with all things in retro computing, enjoy it while it works. 


## OTHER NOTES

RAD size could likely be optimised a little more by reducing sector size on >2.0 systems
but this does not appear to be possible (mount fails when SectorSize = 256). 

Another option to reduce RAD size could be a compressed boot image that unpacks to RAM
at boot time but LhA executable is already as large as current RAD. 





