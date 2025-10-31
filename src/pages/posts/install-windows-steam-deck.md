---
layout: ../../layouts/BlogLayout.astro
title: How to install Windows or Ubuntu on a Steam Deck with an External USB Drive
tags: [gaming, steam deck]
published: 'January 29 2023'
modified: 'September 05 2023'
---

If you want to save your Steam Deck's storage, particularly when equipped with only 64GB, while also setting up Windows or Linux as a secondary operating system, this guide show you how to install both options on external drive.

## Windows Installation

To run Windows from an USB drive, you'll need to use Windows to Go as standard versions cannot be installed on external drives. An SSD is recommended. Download the [Windows 11 ISO](https://www.microsoft.com/en-us/software-download/windows11) from Microsoft's website, and [Rufus](https://rufus.ie/) to create Windows to Go image option.

Once you have both the Windows ISO and Rufus ready:

1. Open Rufus and select the external USB drive as the target device.
2. Choose the Windows 11 ISO as the source.
3. In the Partition scheme section, select "MBR partition scheme for BIOS or UEFI computer."
4. Choose NTFS as the file system.
5. In the Boot selection section, select Windows to Go.
6. Click the Start button in Rufus to begin the process.
7. Once Rufus finishes, you can install Windows 11 by pressing the volume and power button on your Steam Deck and selecting the USB drive as the boot option.

**Dual Boot**

Dual boot Windows 11 and SteamOS on Steam Deck is a little more involved, refer to [Steamdeck Ultimate Windows 11 Guide](https://github.com/baldsealion/Steamdeck-Ultimate-Windows11-Guide/wiki).

## Ubuntu Installation

**Notes**: This step isn't needed on Ubuntu 25. The standard installation should work fine. Just select the external drive, delete any existing partitions, and create a new one using Ext4 with the mount point "/". The boot partition will be created automatically.

If you install Ubuntu by selecting the external drive as its destination, it may still prompt you to select Ubuntu boot options even when the external drive is not connected. To avoid this issue, disable the ESP flag during the installation process. Here are the steps:

- Create a live USB Ubuntu by downloading [Ubuntu ISO](https://ubuntu.com/download/desktop) and [Etcher](https://etcher.balena.io/)
- Plug both live USB and the empty drive into Steam Deck
- Boot into Ubuntu by holding volume button and power button
- Choose try Ubuntu
- Open GParted, find the partition flagged as ESP, click on manage flags and disable it. (step by step details here [Install Ubuntu on USB](https://itsfoss.com/intsall-ubuntu-on-usb/))
- Once removed, select "Install Ubuntu" on the desktop
- Skip wifi setup and choose "Minimal installation", then "Something else"
- Choose the correct external drive for "Device for bootloader installation" (for example /dev/sda)
- On this drive, clicking the – button to delete any existing partitions
- Select + button to create partition for ESP, set size 100-500 MB and use as "EFI System Partition"
- Create the remaining free space with Ext4 filesystem with mount point "/"
- When the installation finishes, click "Continue Testing" and re-enable ESP flags in GParted.

Your Steam Deck still boots into SteamOS the way it does, and Ubuntu only shows up in the Boot Manager if you plug in the external drive.

**Removing Ubuntu from BIOS Boot Menu (UEFI)**

If you mistakenly added Ubuntu to the boot menu in your BIOS or UEFI, you can remove it.

```bash
sudo efibootmgr
# Then delete the option you don't want. In this example, Ubuntu is entry 0.
sudo efibootmgr -b 0 -B 
```

Then go to `rootfs/mnt/efi`, you should find something like `boot`, `steamos`, `ubuntu`. Delete `ubuntu`.

**Fixing SteamOS Boot Failure**

If you encounter a "Default Boot Device Missing or Boot Failed" error after a SteamOS update:

- Power off your Steam Deck and access the boot menu by holding Volume Up and Power.
- Choose "Boot From File" to open a File Explorer.
- Select the first .esp file, open the EFI partition, and boot from the SteamOS .efi file.
- Switch to SteamOS Desktop, open Konsole, and execute (assuming 0001 isn't in use, check `efibootmgr` first):

```bash
sudo efibootmgr -c -L "SteamOS" -l "\EFI\steamos\steamcl.efi" -d /dev/nvme0n1p1 -b 0001
```

**Setting SteamOS as the default**

<https://github.com/scawp/Steam-Deck.Force-SteamOS-On-Boot>

<https://github.com/ryanrudolfoba/SteamDeck-EFI-script>

*NOTE: If you encounter boot issues after unplugging and re-plugging an external drive, update the SSD enclosure firmware (I have UGREEN for example). Find out what the chipset is, and get the newest from [station-drivers](<https://www.station-drivers.com/index.php/en/component/remository/Drivers/Realtek/NVMe-USB-3.1/lang,en-gb/>)*

*UPDATE: If you prefer, you can run Windows inside Ubuntu using Docker. I’ve tested it—it’s slow, but it works for running some Windows programs. Follow the instructions here: https://github.com/dockur/windows/*