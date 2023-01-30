---
layout: post
tags: [gaming, steam deck]
---
#

Installing Windows 11 or Ubuntu on an external USB drive is a great way to expand the capabilities of your Steam Deck, especially if you have the 64GB version. This guide provides instructions for installing either operating system on an external USB drive for use with your Steam Deck.

## Windows Installation

To run Windows from an external USB drive, you'll need to use Windows To Go. First, download the [Windows 11 ISO](https://www.microsoft.com/en-us/software-download/windows11) from Microsoft's website. Then, get [Rufus](https://rufus.ie/), a free and open-source utility for creating bootable USB drives. Note: The easiest way to use Rufus is with a Windows PC, as it is designed for Windows. If you are unable to find one, you might run it on Steam Deck with Lutris

Once you have both the Windows 11 ISO and Rufus, follow these steps:

1. Connect the external USB drive to your Steam Deck.
2. Open Rufus and select the external USB drive as the target device.
3. Choose the Windows 11 ISO as the source.
4. In the Partition scheme section, select MBR for a BIOS computer or UEFI for an UEFI computer.
5. Choose NTFS as the file system.
6. In the Boot selection section, select Windows to Go.
7. Click the Start button in Rufus to begin the process.
8. Once Rufus finishes, you can install Windows 11 by pressing the volume and power button on your Steam Deck and selecting the USB drive as the boot option.

### Dual Boot

If you want to dual boot Windows 11 and Ubuntu on your Steam Deck, the process is a little more involved. You can refer to [Steamdeck Ultimate Windows 11 Guide](https://github.com/baldsealion/Steamdeck-Ultimate-Windows11-Guide/wiki).

# Ubuntu Installation

Normally, Ubuntu will prompted to select boot options every time you start up your Steam Deck, which can be annoying. To avoid this issue, you can disable the ESP flag during the installation process by following the guidelines outlined in this [Install Ubuntu on USB](https://itsfoss.com/intsall-ubuntu-on-usb/)

### Removing Ubuntu from BIOS Boot Menu (UEFI)

If you mistakenly added Ubuntu to the boot menu in your BIOS or UEFI, you can find how to remove it [here](https://askubuntu.com/questions/63610/how-do-i-remove-ubuntu-in-the-bios-boot-menu-uefi).