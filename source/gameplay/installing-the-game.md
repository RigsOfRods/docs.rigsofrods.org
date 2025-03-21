# Installation Guide

To effortlessly install and keep Rigs of Rods up-to-date, we recommend using the [itch.io](https://itch.io/app) desktop app available for Windows and Linux.

[![Available on itch.io](https://static.itch.io/images/badge-color.svg){ width=150 loading=lazy }](http://rigs-of-rods.sf.net/itch/dev/)

!!! danger "Don't place your device at risk"
    For your security, only download Rigs of Rods from the [official Download Center](https://www.rigsofrods.org/download). Downloading from unknown sources may expose you to malware, outdated versions, or modified files that could harm your device.

## Windows


!!! warning ""Windows protected your PC" Windows SmartScreen"
    On Windows, you may be presented with a pop up saying that it prevented an unrecognized app from starting. You must click **More info** and then **Run anyway** in order for the installer to run.

### with Installer <small>recommended</small> { #with-installer data-toc-label="with Installer" }

<figure markdown>
  ![Install guide](../images/win-install-ror.gif){ loading=lazy }
  <figcaption>Windows 11 version 21H1</figcaption>
</figure>

For the latest version, go to the [Download Center](https://www.rigsofrods.org/download) and select *Rigs of Rods 64-bit Installer* for Windows. You will immediately be redirected to SourceForge, and the download will automatically begin.

When your download finishes, follow these steps to quickly go through the installer.

1. Select your language, by default it is English. Click *Next*.
2. Accept the License Agreement by selecting *I accept the agreement* then click *Next*.
3. If you wish to install to another location, select *Browse*, otherwise the default location will be used.
4. If you want the installer to create a desktop shortcut check *Create a desktop shortcut*.
5. Review the installation and click *Back* if you want to make any changes, otherwise click *Install* to begin the installation process.
6. Upon completion of the installation read then click *Next*.
7. Well done, the installation is now completed. Leave *Launch Rigs of Rods* checked and click *Finish* to launch Rigs of Rods.


### with Portable (.zip)

For the latest version, go to the [Download Center](https://www.rigsofrods.org/download) and select *Rigs of Rods 64-bit Portable (.zip)* for Windows. You will immediately be redirected to SourceForge, and the download will automatically begin.

When your download finishes, follow these steps to launch Rigs of Rods.

1. Extract the .zip into your desired location (Do not merge with an existing Rigs of Rods version!)
2. Launch Rigs of Rods by double-clicking `RoR.exe`

## Linux

### with Portable (.zip) <small>recommended</small> { #with-portable-zip_1 data-toc-label="with Portable (.zip)" }

For the latest version, go to the [Download Center](https://www.rigsofrods.org/download) and select *Rigs of Rods 64-bit Portable (.zip)* for Linux. You will immediately be redirected to Sourceforge, and the download will automatically begin.

When your download finishes, follow these steps to launch Rigs of Rods on Linux.

1. Extract the .zip into your desired location (Do not merge with an existing Rigs of Rods version!)
``` bash
unzip rigs-of-rods-linux.zip
```
4. It may not always be necessary, but grant the execute permission to the executable and script run file.
```bash
chmod +x ./RoR
chmod +x ./RunRoR
```
3. Depending on your graphical interface, you may double-click `RunRoR` or run from the terminal.
``` bash
./RunRoR
```

### with Snap Store

**Snap Store is not OFFICIALLY maintained but is regularly kept up-to-date.** Snaps can be used on all major Linux distributions and is widely used because of its graphical counterpart the Snap Store.

``` bash
sudo snap install rigs-of-rods
```

### with AUR

The Arch User Repository (AUR) packages can be installed on your Arch Linux system with with the use of a helper like yay or paru.

```bash
paru -S rigsofrods
```
## Development Builds

If you want to try out the latest changes without waiting for a stable release, you can use the development builds. These builds include new features, bug fixes, and improvements but may also be unstable.

!!! warning "Try at your own risk!"
    These builds allow you to experience new changes before they are officially released. These builds are not thoroughly tested, so the chance you may experience crashes, bugs, or other issues is higher than with stable versions. If you encounter problems, consider reporting them on the [Rigs of Rods GitHub issues](https://github.com/RigsOfRods/rigs-of-rods/issues) page.

### with itch.io Desktop App <small>recommended</small> { #with-itch-io-desktop-app }

Just like the stable release, the development builds are available through the itch.io app. After every code change, the builds are automatically pushed to itch.io and delivered as an optional update for you.

[:fontawesome-solid-download: Download Rigs of Rods Experimental](http://rigs-of-rods.sf.net/itch/dev/){ .md-button .md-button--primary }

### with itch.io (.zip)

If you prefer not to use the the desktop app, you can still download the builds manually.

1. Go to the the [Rigs of Rods itch.io build page](https://rigs-of-rods.itch.io/rigs-of-rods-dev).
2. Download the development builds for Windows or Linux.
3. Extract the contents to a preferred location.
4. Run `RoR.exe` (Windows) or `./RunRoR` (Linux) to start the game.

Refer to previous sections of this guide for additional guidance on launching the game. If you have any issues with development builds (such as broken links or missing builds) please [refer to this thread](https://forum.rigsofrods.org/threads/ror-development-builds-for-windows-and-linux.696/) on the community forums. 
