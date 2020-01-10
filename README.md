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
The intel nuc comes with a vesa mount which i mounted onto my monitor which makes it compact and hidden. I am using a ethernet cable connected to my main PC which allows me to get internet.

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

