## ElimuPi

The purpose of this project is to provide a DEAN digital classroom environment for educational project in Tanzania and Kenya. This includes providing full Android tablet support without any direct internet connectivity.

Please visit https://www.dean.ngo/solutions/elimupi/  for more information.

## Introduction

This version of the ElimuPi build supports:

- [F-Droid](https://f-droid.org/) an Android application store.
- Web pages for management of the system and content management (WordPress).
- WiKiPedia alike functions based on [Kiwix](https://www.kiwix.org/en/about/).
- [Kolibri](https://learningequality.org/kolibri/) learning system.
- Dynamic content addition through USB storage.
- Secured WiFi Access Point.
- Wifi client support that defaults connects to AP's: elimupi-connect or dean-4g.
- Local DHCP, DNS.
- [Scratch](https://scratch.mit.edu/about), a high-level block-based visual programming language.
- Beamer support via onboard micro HDMI

#  Installation

## Prerequisites:
 - PC or laptop with Linux, Windows with [WSL](https://ubuntu.com/wsl) or MacOS operating system installed.
 - A Raspberry Pi model 5 with a wired TCP connection to LAN.
 - A Micro SD-card class 10 > 8GB.
 - Git installed.
 - Ansible 2.10 > installed.
 - [ssh_askpass](https://packages.ubuntu.com/search?keywords=ssh-askpass) installed.
 - [Raspberry Pi Imager](https://www.raspberrypi.com/software/)  installed.
 - [Raspberry Pi OS Lite 64 bits image , Release date:  November 19th 2024.](https://downloads.raspberrypi.com/raspios_lite_arm64/images/raspios_lite_arm64-2024-11-18/2024-11-13-raspios-bookworm-arm64-lite.img.xz)

 - Ansible vault password ( contact DEAN development)

## Install Raspberry Pi OS

 - Use Raspberry PI Imager to write the downloaded image to the SD-card using instructions at  https://www.raspberrypi.com/documentation/computers/getting-started.html#installing-the-operating-system.
 - Insert the SD-card.
 - Start Raspberry PI Imager.
 - Under **Raspberry Pi Device** select **Raspberry Pi 4**.
 - Under **Operating system** select **Choose OS --> Use Custom** and select the downloaded image - [Raspberry Pi OS Lite 64 bits image , Release date: November 19th 2024.](https://downloads.raspberrypi.com/raspios_lite_arm64/images/raspios_lite_arm64-2024-11-18/2024-11-13-raspios-bookworm-arm64-lite.img.xz)
 - Under **Storage** and select the SD-card device.
 - Select **Advanced options** -->  **Enable SSH** --> **Use password authentication**.
 - Set **Username** to: **pi** and **Password** to : **elimupi** and select **SAVE**.
 - Select **WRITE**.

 When the image has been successfully written insert the SD-card into the Raspberry Pi and boot the device connected to local LAN.

## Build ElimuPi Image

Provision the ElimuPi software by running the ansible-play book against local Raspberry Pi and build Elimupi the image.

 - Find the Pi's assigned IP address on your local LAN. ( via Wifi router or a nmap).
 - Git clone this repo and cd elimupi/ansible directory of this repo.
 - Adjust the current IP adresss of key : ansible_host  in file  inventory.yml to your Pi's local assigned IP address.
 - Increment version release number variable, **elimupi_release**: in file ansible/group_vars/all/vars.yml if needed.
 - Install Ansible collections:

`ansible-galaxy collection install -r collections.yml`

 - Install Ansible roles.

`ansible-galaxy install -r roles.yml`

 - Run playbook

`ansible-playbook -i ./inventory.yml playbook-raspberrypi.yml --ask-vault-pass`

The installation will take approximately 20 minutes to finish and there shouldn't be any errors.

## Create ElimuPi image copy

 - Create a image copy of the SD-card with the ElimuPi software installed using instructions at https://beebom.com/how-clone-raspberry-pi-sd-card-windows-linux-macos/
 - Shrink cloned the image file (Linux Only) using [PiShrink](https://github.com/Drewsif/PiShrink) and the compression option -Za
 - Name the image: **ElimuPi_Image_<YYYY-MM-DD>-raspios-bookworm-arm64_lite_Release_<-Version->.img.xz** e.g.

This should produce a xz compressed Elimupi image file.

The image file can than be directly written to other SD-cards using Raspberry Pi Imager selecting the image with Use Custom Operation System option.

# Connecting to Elimupi

-  Disconnect the Raspberry PI's TCP wired connection.
-  Connect your device via WiFi to SSID:  **elimu** using passcode: **1234567890**
-  Point your browser to http://start.elimupi.online

## Default users
All default username and passwords will be **pi/elimupi** unless noted differently.

The default password for the Wifi AP with SSID: 'elimu' is : 1234567890

## User access
The end users can access the available resources after they are connected to the Wifi network.

The following links are provided to access the resources:

- **Main interface** - [start.elimupi.online](http://start.elimupi.online)
- **Kolibri** - [kolibri.elimupi.online](http://kolibri.elimupi.online)
- **Kiwix** - [wiki.elimupi.online](http://wiki.elimupi.online)
- **Fdroid** - [fdroid.elimupi.online](http://fdroid.elimupi.online)
- **Files** - [files.elimupi.online](http://files.elimupi.online)
- **Moodle** - [moodle.elimupi.online](http://moodle.elimupi.online)
- **Admin** - [admin.elimupi.online](http://admin.elimupi.online)
- **Scratch** - [scratch.elimupi.online](http://scratch.elimupi.online)

After you finished the installation you need to visit [admin.elimupi.online](http://admin.elimupi.online) login with the Admin account and go to Manage --> "Please follow the directions to register your device, so that it can synchronize with the central server."

## Notes
**NOTE1**: This install is tested to work with [Raspberry Pi OS Lite 64 bits image , Release date: November 19th 2024.](https://downloads.raspberrypi.com/raspios_lite_arm64/images/raspios_lite_arm64-2024-11-18/2024-11-13-raspios-bookworm-arm64-lite.img.xz) on a Raspberry Pi model 5.
