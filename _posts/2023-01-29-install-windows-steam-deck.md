---
layout: post
title: How to install Windows or Ubuntu on a Steam Deck with an External USB Drive
tags: [gaming, steam deck]
---

Installing Windows or Ubuntu on an external USB drive is a great way to save your Steam Deck storage, especially if you have the 64GB version. This guide provides instructions for installing either operating system on your Steam Deck.

## Windows Installation

To run Windows from an USB drive, you'll need to use Windows to Go as standard versions cannot be installed on external drives. An SSD is also recommended as HDD can be slow. Download the [Windows 11 ISO](https://www.microsoft.com/en-us/software-download/windows11) from Microsoft's website, and [Rufus](https://rufus.ie/) to create Windows to Go image option.

Once you have both the Windows ISO and Rufus, follow these steps:

1. Open Rufus and select the external USB drive as the target device.
2. Choose the Windows 11 ISO as the source.
3. In the Partition scheme section, select "MBR partition scheme for BIOS or UEFI computer."
4. Choose NTFS as the file system.
5. In the Boot selection section, select Windows to Go.
6. Click the Start button in Rufus to begin the process.
7. Once Rufus finishes, you can install Windows 11 by pressing the volume and power button on your Steam Deck and selecting the USB drive as the boot option.

**Dual Boot**

If you want to dual boot Windows 11 and SteamOS on your Steam Deck, the process is a little more involved. You can refer to [Steamdeck Ultimate Windows 11 Guide](https://github.com/baldsealion/Steamdeck-Ultimate-Windows11-Guide/wiki).

## Ubuntu Installation

If you install Ubuntu the normal way, it will prompted to select boot options every time you start up your Steam Deck. To avoid this issue, you can disable the ESP flag during the installation process. Here are the steps:

- Create a live USB Ubuntu by downloading [Ubuntu ISO](https://ubuntu.com/download/desktop) and [Etcher](https://etcher.balena.io/)
- Plug both live USB and the empty drive into Steam Deck
- Boot Steam Deck into Boot Manager by holding volume up button and power button and select Ubuntu
- Choose try Ubuntu
- Disable ESP and install Ubuntu on the second drive (follow this guide [Install Ubuntu on USB](https://itsfoss.com/intsall-ubuntu-on-usb/))
- When the installation finishes, reset ESP partition back in its original state.

Your Steam Deck still boots into SteamOS the way it does, and Ubuntu only shows up in the Boot Manager if you plug in the external drive.

**Removing Ubuntu from BIOS Boot Menu (UEFI)**

If you mistakenly added Ubuntu to the boot menu in your BIOS or UEFI, you can find how to remove it .

```bash
sudo apt-get install efibootmgr
sudo modprobe efivars
sudo efibootmgr
# Then delete the option you don't want. In this example, Ubuntu is entry 0.
sudo efibootmgr -b 0 -B 
```

Further details described in [remove Ubuntu in boot menu](https://askubuntu.com/questions/63610/how-do-i-remove-ubuntu-in-the-bios-boot-menu-uefi)

Now you can enjoy either Windows 11 or Ubuntu on your Steam Deck.
