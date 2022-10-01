General FAQ
============



Welcome to the General FAQ! Here you'll find answers to common questions and errors.
It is organized into sections to make finding answers easier.

## Supported operating systems 
 
Rigs of Rods is officially supported on 64 bit Windows 7 SP1, Windows 8/8.1, Windows 10, and Linux.

Windows XP & Vista are no longer supported as of version 0.4.8 RC5. 

32 bit is no longer supported as of version 2020.01.

ChromeOS (Chromebooks), MacOS, and mobile platforms (Android/iOS) are not supported and most likely never will be.

## Downloading Rigs of Rods

#### Windows

You can find the latest version on the [home page](https://www.rigsofrods.org/). If you need help, check out the [Beginner's Guide](/gameplay/beginners-guide/).

#### Linux

Linux users can download the latest version from [Itch.io](https://rigs-of-rods.itch.io/rigs-of-rods).

It is recommended to install using the [Itch desktop app](https://itch.io/app).

#### Development builds 

If you want to try the latest changes to RoR, you can download a [development build](https://forum.rigsofrods.org/threads/ror-development-builds-for-windows-and-linux.696/).


#### Old versions 

You can find old RoR versions on [SourceForge](https://sourceforge.net/projects/rigsofrods/files/rigsofrods/). These versions are entirely unsupported!

## Mods

#### Downloading mods

You can find mods on the [Repository](https://forum.rigsofrods.org/resources/), the [content](https://forum.rigsofrods.org/#repository.11) section of the forum, and the [archives](https://archives.rigsofrods.net).

For help with installing mods, see [this page](/gameplay/installing-content/).

#### Archives

You can find links to the archives [here](https://archives.rigsofrods.net). These contain content from previous versions of the website.

## Multiplayer

To play multiplayer, see [this section](/gameplay/beginners-guide/#multiplayer) of the Beginner's Guide.

**Please know that multiplayer is still a work-in-progress, and crashes may happen.**

#### Wrong server version

This means you're trying to join a server that is running an older or newer RoRNet version than what your current RoR version supports.

The latest version, 2022.04, supports RoRNet 2.43.


## Errors & glitches

These errors may occur when launching RoR. 

#### No render system plugin available

![error_no_rendersys_avail](/images/error_no_rendersys_avail.png)

![error_no_render_sys_selected](/images/error_no_render_sys_selected.png)

If you downloaded RoR using the zip file, you may receive these errors. This is caused by the DirectX 9 Runtime not being installed. Install it from [Microsoft's website](https://www.microsoft.com/en-us/download/details.aspx?id=8109) then restart your PC.


#### MSVCP DLLs missing

When launching RoR, you may receive a MSVCP140.dll/MSVCP110.dll/MSVCP100.dll error.

This is caused by the required Visual C++ x86/x64 Redistributable not being installed. 

Install the correct version that matches the `.dll` name in the error then restart your PC.

When the site asks what version to download, just install both. 

Latest release:

- [MSVCP140.dll](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#visual-studio-2015-2017-2019-and-2022)  (Select the x64 version)

Older versions:

- [MSVCP110.dll](https://www.microsoft.com/en-us/download/details.aspx?id=30679)

- [MSVCP100.dll](https://www.microsoft.com/en-us/download/details.aspx?id=26999)


#### Special characters crash (Cannot open controller input map)

![error](/images/error-special-chars.png)

![error2](/images/error-generatecontent.png)

This is caused by having [Unicode](https://en.wikipedia.org/wiki/Unicode) characters in the path to the `Documents\My Games\Rigs of Rods` folder, usually caused by the  Windows username (e.g. `Usér`).  

This will be fixed in a future version. For now, there is a workaround with two methods. Choose the second method if you don't want RoR to run as administrator.

##### Method 1
1. Inside the installation directory, where RoR.exe is (usually `C:\Program Files\Rigs of Rods`) create a folder named `config` <br>
2. Right click `RoR.exe` and click `Properties` <br>
3. Under the `Compatibility` tab, check the `Run this program as administrator` box, then click `Apply` and close the window.  <br>


##### Method 2
1. Move any mods from the `Documents\My Games\Rigs of Rods\mods` folder if you have any installed<br>
2. Uninstall RoR from Windows settings, then remove the `Documents\My Games\Rigs of Rods` folder if required<br>
3. Download the zipped release from [Itch.io](https://rigs-of-rods.itch.io/rigs-of-rods) and extract `rigs-of-rods-windows.zip` into any directory that isn't in Program Files or the users folder (Documents, Downloads, etc). <br>
Example: `C:\Games` <br>
4. Inside the extracted folder, create a folder named `config` <br>
5. Launch the game by double clicking `RoR.exe`. You can optionally create a shortcut by right clicking.<br>

RoR will now use the `config` folder instead of the default `Documents\My Games\Rigs of Rods` folder. 

If you installed the content packs, you will have to move the `*.zip` files from `Documents\My Games\Rigs of Rods\mods` to `config\mods`. New mods are also installed there.

#### Full screen crash (Cannot create device)

![error-createdevice](/images/error-createdevice.png) 

This error is usually caused by enabling full screen with the wrong resolution (video mode) set. 

1. Browse to `Documents\My Games\Rigs of Rods` and delete the `config` folder inside.
2. Start RoR, the game will be in a small window. Click Settings -> Render system and change the Video Mode setting to your monitor's native resolution. Enable full screen if you want.
3. Restart RoR.

If this doesn't fix your error, then your GPU is most likely too old to run RoR. 

#### Null program bound

![error-nullprogrambound](/images/error-nullprogrambound.png)

This error occurs with some Intel integrated graphics chips. Unfortunately there's currently no fix.

More info: [GitHub issue](https://github.com/RigsOfRods/rigs-of-rods/issues/2385)

#### Glitchy vehicle shadows

With some GPUs (mostly integrated ones), shadows on vehicles may appear glitchy: 

![shadows-glitch](/images/shadows-glitch.gif)

This is caused by your GPU not supporting self-shadowing (Shadows from other objects casting onto the vehicle). Please try one of the following workarounds:

##### #1: Disable shadows 

The simplest workaround is to just disable shadows. (Settings -> Graphics -> Set shadows to "None" -> Restart RoR).

##### #2: Enable classic materials
 
Starting with version 2020.01, an option to enable classic (0.38-era) material shaders is available. This can be found under Settings -> Graphics -> Classic material shaders. 

Currently they do not support self-shadowing, so the glitch is not present using these.

##### #3: Disable self-shadowing from default materials 

If you prefer to use the default materials instead, do the following: 

1. Browse to where RoR is installed. This is usually `C:\Program Files\Rigs of Rods` by default. 

2. Open the `resources` folder, followed by the  `managed_materials` folder. 

3. Copy the `managed_mats_vehicles.material` file onto your Desktop. 

4. Open the file with Notepad (Right click -> Open with -> Notepad)

5. Add `//` to the beginning of the first line: `//import * from "shadows.material"`

6. Save the file, then copy it back to `resources\managed_materials`, overwriting the original file. Allow administrator permission when prompted.


#### Airplane spawning crash

If the game crashes when spawning an aircraft, change the Lights setting (Graphics tab) to anything that isn't `None (fastest)`:

![airplane-crash-lights-fix](/images/airplane-crash-lights-fix.png)


## Miscellaneous

#### Reporting bugs

You can report bugs and other issues on RoR's [GitHub repo issue tracker.](https://github.com/RigsOfRods/rigs-of-rods/issues) 

Make sure your issue hasn't already been reported.

**The issue tracker is only for issues relating to the latest development build, if you're using an official release, please post on the [correct support forum](https://forum.rigsofrods.org/#troubleshooting.7) instead.** 
