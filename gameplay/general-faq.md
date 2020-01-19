---
layout: page
title:  "General FAQ"
categories: [gameplay]
---

<div class="toc" markdown="1">
  * TOC
  {:toc}
</div>

Welcome to the General FAQ! Here you'll find answers to common questions and errors.
It is organized into sections to make finding answers easier.

# Supported operating systems 
 
Rigs of Rods supports 64 bit Windows 7 SP1, Windows 8/8.1, Windows 10, and Linux.

Windows XP & Vista are no longer supported as of version 0.4.8 RC5. 

32 bit is no longer supported as of version 2020.01.

ChromeOS (Chromebooks), MacOS, and mobile platforms (Android/iOS) are not supported and most likely never will be.

# Downloading Rigs of Rods

### Windows

You can find the latest version on the [home page](https://www.rigsofrods.org/). If you need help, check out the [Beginner's Guide](/gameplay/beginners-guide/).

### Linux

Linux users can download the latest version from [Itch.io](https://rigs-of-rods.itch.io/rigs-of-rods).

It is recommended to install using the [Itch desktop app](https://itch.io/app).

### Development builds 

If you want to try the latest changes to RoR, you can download a [development build](https://forum.rigsofrods.org/threads/ror-development-builds-for-0-4-8-for-windows-and-linux.696/).


### Old versions 

You can find old RoR versions on [SourceForge](https://sourceforge.net/projects/rigsofrods/files/rigsofrods/). These versions are entirely unsupported!

# Mods

### Downloading mods

You can find mods on the [Repository](https://forum.rigsofrods.org/resources/), the [content](https://forum.rigsofrods.org/#repository.11) section of the forum, and the [archives](https://archives.rigsofrods.net).

For help with installing mods, see [this page](/gameplay/installing-content/).

### Archives

You can find links to the archives [here](https://archives.rigsofrods.net). These contain content from previous versions of the website.

# Multiplayer

To play multiplayer, see [this section](/gameplay/beginners-guide/#multiplayer) of the Beginner's Guide.

**Please know that multiplayer is still a work-in-progress, and crashes may happen.**

### Wrong server version

This means you're trying to join a server that is running an earlier/later RoRNet version than what your current RoR version supports.

The latest version, 2020.01, supports RoRNet 2.42.


# Errors

### MSVCP DLLs missing

When launching RoR, you may receive a MSVCP140.dll/MSVCP110.dll/MSVCP100.dll error.

This is caused by the required Visual C++ x86/x64 Redistributable not being installed. 

Install the correct version that matches the `.dll` name in the error then restart your PC.

When the site asks what version to download, just install both. 

- [MSVCP140.dll](https://www.microsoft.com/en-us/download/details.aspx?id=48145)

- [MSVCP110.dll](https://www.microsoft.com/en-us/download/details.aspx?id=30679)

- [MSVCP100.dll](https://www.microsoft.com/en-us/download/details.aspx?id=26999)


### Cannot open Xbox 360 input map 
### Failed to generate list of installed content

When you launch RoR, you may receive the following errors:

![error](/images/error-special-chars.png)

![error2](/images/error-generatecontent.png)

This is caused by having special characters in your Windows username (e.g. `Usér`).  

Current workaround:

1. Inside the installation directory, where RoR.exe is (usually `C:\Program Files\Rigs of Rods`) create a folder called `config`
2. Right click `RoR.exe` and click `Properties`
3. Under the `Compatibility` tab, check the `Run this program as administrator` box, then click `Apply` and close the window. 

RoR will now use the `config` folder instead of the default `Documents\Rigs of Rods 0.4` folder. 

If you installed the content packs, you will have to move the `*.zip` files from `Documents\Rigs of Rods 0.4\mods` to `config\mods`. New mods are also installed there.

# Miscellaneous

### Reporting bugs

You can report bugs and other issues on RoR's [GitHub repo issue tracker.](https://github.com/RigsOfRods/rigs-of-rods/issues) 

Make sure your issue hasn't already been reported.

**The issue tracker is only for issues relating to the latest development build, if you're using an official release, please post on the [correct support forum](https://forum.rigsofrods.org/#troubleshooting.7) instead.** 