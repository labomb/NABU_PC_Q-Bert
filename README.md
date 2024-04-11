# Q*Bert for the NABU PC
 

![Q*Bert](/assets/images/qbert.jpg)
 
 
This repository contains all of the necessary source code and tools required to build Q*Bert for the NABU PC in a CP/M development environment. 

The original Q*Bert source files were recovered (no easy task when working with 40+ year old hardware and disks!) and graciously made available by Leo Binkowski, one of the original programmers who worked at NABU back in the early 80's, and the original author of this program. To learn more about Leo, I recommend that you visit his YouTube channel found [here](https://www.youtube.com/@leo.binkowski), and also take a peek [here](https://nabu.ca/leo-s-tales) as well.

The source code that was initially made available was mostly complete, but alas there were several issues that prevented it from properly building or running on the NABU PC. With that, I spent a some time pouring through the code and fixing the issues that I found, reorganizing things a bit, re-creating missing source files, and documenting in a bit more detail on how to go about building and running Q*Bert. The result of those efforts are presented here. Additionally, Leo has incorporated all of the required patches into his github repository (found [here](https://github.com/LeoBinkowski/NABU/tree/main)), so you can grab working code from there as well.

 
## Directories

* All the required sources files and build scripts are in the root directory of this repository
* The 'tools' directory contains the CP/M development tools required to build Q*Bert
* The 'extras' directory contains a copy of the NABU main menu 'Cycle 1' software (see below)
* The 'unused' directory contains files that were part of the original source repository, but aren't actually required/used to build the Q*Bert application

 
## Prerequisites

* You will need a CP/M development environment or tools that enable running the native CP/M tools (provided in this repository) on various host platforms. While it is beyond the scope of this document to provide all of the details on how to set such an environment up, there are numerous options available. Feel free to search for [AltairZ80](https://schorn.ch/altair.html), [RunCPM](https://github.com/MockbaTheBorg/RunCPM), [myZ80](http://www.z80.eu/myz80cpm.html), [ZXCC](https://www.seasip.info/Unix/Zxcc/), and several others. Or if you are a traditionalist, you can certainly use a real CP/M computer!
* You will also need a means to load the resulting Q*Bert 'PAK' file after building onto the NABU PC. Most, if not all of the NABU server software applications available include the ability to load local applications. The approach that I use is detailed below, but refer to your specific server documentation for details on how to do so.

 
## Building

Building Q*Bert is quite straight-forward:

#### Assemble and link

If you have the disk space required to assemble the entire source all at once, you can simply do this:

1. Copy all of the source files and all of the files in the tools directory to a disk, disk image, hard drive image, or directory depending on your CP/M build environment.
2. Assemble and link the sources.
	- If you have CP/M 2.2 or CP/M 3 (sometimes referred to as CP/M Plus) or equivalent, you can simply enter something like this:
      ```
      SUBMIT DOALL
      ```
	- Or if you prefer, you can enter each of the commands listed in the DOALL.SUB file individually:
      ```
      M80 =LINKTAB.MHO
      M80 =QSCREEN
      M80 =QBOARD
      .
      and so on...
      .
      L80 QBERT1,QBERT2,QBERT/N/Y/E:QSCREE
      ```

Once the above steps are completed, you will have a new file named QBERT.COM.

 
#### Create a .PAK segment file

You now need to convert the QBERT.COM file into a 'PAK' file that is suitable for loading onto the NABU PC. Note that QBERT.COM in it's current state is *not* a standard CP/M executable that can simply be run from the CP/M command line, it needs to be converted and loaded instead. The tool that does the conversion is CABUILD.

When CABUILD is executed, it will prompt you for various bits of detail that it requires to create the PAK file:

 
![CABUILD.COM](/assets/images/cabuild.jpg)
 

A new file named 00015C.PAK will be created when the process is complete.

 
## Running

For this project, I used the NABU Internet Adapter server software found [here](https://nabu.ca/downloads-nabu-internet-adapter). If using another server application, you may need to take a different approach.

Copy the 00015C.PAK file, along with the 000001.PAK file found in the extras folder of this repository, to the directory that you have configured as your 'local PAK folder' in the IA application. Be sure to configure the IA via Settings to 'Use local folder for HomeBrew' in the Source menu, and verify that the local folder that is set there is correct for your setup.

Assuming your NABU is connected and working properly, you should be able to restart it and subsequently see the (hopefully now familiar) main menu, or 'Cycle 1' software interface as per usual. Navigate to the 'NETWORK SERVICES' menu item, and then select 'Q*BERT'. You should be good to go :slightly_smiling_face:.

 
## Note

You should maintain the line ($0D and $0A) and file ($1A) termination format of the source files should you wish to modify them at some point. Some CP/M build environments can handle files regardless, while others cannot. If you see multiple errors with a given file during assembly, check the file formatting.

 
## Original NABU Q*Bert Z80 Source code

The official Source Code to NABU Q*Bert can be found [here](https://github.com/LeoBinkowski/NABU/tree/main).

The authors are:

- Leo Binkowski
- Tim Ranger

of the NABU Network of Ottawa Canada, 1982-1984

 
## Bug reports, feedback, etc...

Please use the [github issues page](https://github.com/labomb/NABU_PC_Q-Bert/issues) to report any problems.

>**Please Note:**
 I cannot provide general support for the NABU PC, it's usage, or issues that you may have with it. Accordingly, I ask that you please not post anything relative to general usage/issues/questions here. There are several other venues for these types of questions, including websites, forums, and a Discord server. Thanks!
 
