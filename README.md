# [Guide] Cheap Hackintosh Build
## Overview
This guide will walk you through the process of creating a hackintosh, on a Intel Nuc. This build can boot 3 OS such as Mac Mojave, Windows 10 and Ubuntu all on the one computer.

## What You Need:
- Apple Computer/Laptop
- At least 8GB USB [2.0]
- Intel Nuc


## Specs
- CPU: Intel Core i3-8109U
- GPU: Intel Iris Plus Graphics 655
- RAM: 8x1 GB 2400MHz
- Storage: 240GB M.2 SSD
I brought a bundle package which cost me a total of $510 for everything.  [Link To Bundle](https://www.ple.com.au/Products/634228/Intel-i3-NUC-Bean-Canyon-Super-Starter-Bundle)

## Setup
The Intel Nuc comes with a vesa mount which i mounted onto my monitor which makes it compact and hidden. I am using a ethernet cable connected to my main PC which allows me to get internet.

## Works
- All USB 3.1 Gen Ports
- Internal microphone
- Audio pass through from HDMI
- USB 3.1 Type-c Hotpluggable
- Ethernet 
- Sleep/wake
- App Store

## Not Working
- Headphone jack
- Thunderbolt 3 hotplugging
- Native Wifi [More down below on a work around]
- Bluetooth
- IMessage
- AirDrop

## Not Tested
- Find my iphone
- Multiple monitors

## Preparation Intel Nuc
BIOS Setting
- BIOS Version 0072
BIOS setup can be accessed by mashing the F2 key while booting up. It will get you to the main BIOS setup screens. To start, choose "Load Defaults" (choose from the menu or press F9 in the BIOS setup).
Then change:

- Boot -> Boot Configuration, disable "Network Boot"
- Devices -> Video, "IGD Minimum Memory" set to 64mb or 128mb
- Devices -> Video, "IGD Aperture Size" set to 256mb
- Power -> Secondary Power Settings, "Wake on LAN from S4/S5", set to "Stay Off"
- Boot -> Secure Boot, disable "Secure Boot"
- Devices -> OnBoard Devices, disable "Bluetooth" (macOS is not compatible well with Intel Wi-Fi/Bluetooth)
- Boot -> Boot Priority -> Legacy Boot Priority, enable "Legacy Boot".

## Preparation USB
1) Plug in your USB at least 8gb in your apple computer and open terminal
2) Type in `diskutil list` and find your USB and take note of the disk number
3) Type in `diskutil partitionDisk /dev/disk2 2 MBR FAT32 "CLOVER EFI" 200Mi HFS+J "install_osx" R` BUT CHANGE `/dev/disk2` to the correct number.
5) You should now have two partitions called `CLOVER EFI` and `install_osx`
6) Download the EFI folder from above and copy the contents into the CLOVER EFI
7) Download MacOS Mojave from the App Store [Link To Mojave](https://apps.apple.com/us/app/macos-mojave/id1398502828?ls=1&mt=12)
8) Once downloaded copy the MacOS Mojave file, (Found in applications folder) to install_oxc
9) Eject USB and your done.

## Installation
1) Plug the USB in one of the 2 front USB prots
2) The clover bootloader screen will show up and you must press space bar on `install_osx` and select verbose boot (This is print out any errors that happen) and click enter on boot with selected options.
3) The system will reboot and you should now see two boot options one being `install_osx` and the other being `Boot MacOS Install From ...` you must go to the settings in clover and change the FakeID to 0x12345678 `Clover Options-> Graphics Injector-> FakeID` and then select `Boot MacOS Install From..` and press enter
4) The MacOS Install screen should pop up you will need to run through the installation and install MacOS to your SSD, once that is done the computer will restart
5) The clover bootloader screen will show up again, select `Boot OS X from (YourPartition)` "YourPartition" will be named depending on what you chose in Disk Utility
6) You should end up at the OS X desktop

## Post Installation
You will need to mount your EFI and copy over your EFI config files from your USB
1) Open Terminal and run `diskutil list` and find your internal storage device and the number of your EFI partition
2) Run `mkdir /Volumes/efi`
3) Mount your EFI `sudo mount -t msdos /dev/disk0s1 /Volumes/efi` (Make sure to replace /dev/disk0s1 to what ever your EFI partition is mount to.)
4) Your EFI should now be mounted and should be on desktop, next you must open the CLOVER EFI and copy over the contents to the EFI.
5) Now you can unplug your USB and you will be able to boot without your USB.

## WIFI Work Around
My WIFI work around involves have another computer close by and an ethernet cable, I connected my Intel Nuc to my other computer running windows (note OS doesn't matter and can be achieved with any OS just a different process). You must then go into the network adaptor settings and find your WIFI connected, you must right click and press properties and on shared, you must enable both setting and under `Home networking connection` select your ethernet adaptor connected to your Intel Nuc. And you should now have internet going to your Intel Nuc



