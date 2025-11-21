---
layout: ../../layouts/BlogLayout.astro
title: How to install Windows on a Steam Deck with an External USB Drive
tags: [gaming, steam deck]
published: 'January 29 2023'
modified: 'September 05 2023'
---
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

## Dual Boot

To dual boot Windows 11 and SteamOS on Steam Deck, refer to [Steamdeck Ultimate Windows 11 Guide](https://github.com/baldsealion/Steamdeck-Ultimate-Windows11-Guide/wiki)
