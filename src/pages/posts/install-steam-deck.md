---
title: 'Installing Non Steam Games on Steam Deck'
layout: ../../layouts/BlogLayout.astro
tags: [gaming, steam deck]
published: 'January 31 2024'
---

Before installing any games on Steam Deck, certain software needs to be installed first. Switch Steam Deck to desktop mode and launch the Discover (Software Center) app. Then, proceed to install the following:

1. **Lutris:**
   Lutris is a game manager that simplifies the installation of various games, including those not natively supported by Steam.

2. **ProtonUp-Qt:**
   Lutris comes with its own Proton (Steam's compatibility tool for running Windows games on Linux), but some games does not work well with it. ProtonUp-Qt allows you to choose and install additional versions. Open ProtonUp-Qt, click "Add version," select "Wine-GE" and choose "GE-Proton8-x." I find that the latest version usually works best, but if your game is not supported, try out other versions.

### Using Lutris for Windows Games

- Open Lutris and click on the + button (Add games to Lutris) in the top-left corner.
- Choose the third option "Install a Windows game from an executable."
- Enter the name of the game and choose the Windows preset if needed.
- Select the Wine setup and specify the location for installation.
- Locate the game setup file (.exe) and click "Install"
- Close the setup window after it's finished.
- A new game should appear in the Lutris Library. You can configure the game banner and add a Steam shortcut if desired. Remember to open and close the Steam app for the changes to take effect.

### Using Lutris for DOS Games

- Open Lutris and click on the + button (Add games to Lutris) in the top-left corner.
- Opt for the last option "Add locally Installed Game"
- Enter the name of the game and select runner as DOSBox (MS-DOS emulator)
- From Game options, select .exe for Main file then click Save
- A new game should appear in the Lutris Library. You can configure the game banner and add a Steam shortcut if desired. Remember to open and close the Steam app for the changes to take effect.

By following these simple steps, you can easily install and play non-Steam games on Steam Deck!
