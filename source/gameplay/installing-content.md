Installing content
============

One of the best features of Rigs of Rods is the vast amount of community-created mods available. This page will tell you everything you need to know about installing mods. You will have to launch RoR at least once for the mods directory to be created.


## In-Game Repository

Starting with Rigs of Rods version 2022.04, it is now possible to download new content from the Repository in-game. 

Just click on the Repository button at the main menu:

![main-menu-repo-button](../images/main-menu-repo-button.png)

You can view different categories, sort by most downloaded/last update/etc, and change the display view.

![in-game-repo](../images/in-game-repo.png)

After you find a mod to install, just click on the file and press the Install button:

![in-game-repo-install](../images/in-game-repo-install.png)

To remove a mod, just go back to the file listing and press Remove. 

### Limitations 
	
- The In-Game Repository currently does not support installing content packs which are a zip file containing other zips. You can still download them in-game, but you'll have to browse to the `mods` folder and extract the pack zip manually. 

- While there is an Addons category, most files there will have to be installed manually. Please see [Installing addons](../tools-tutorials/addons.md) for more information.

## Installing mods manually

Adding a new vehicle or terrain is very simple. Follow the appropriate instructions for your operating system.

### Windows 

First, open File Explorer by clicking the ![File Explorer Icon](../images/file-explorer.png) icon on your taskbar or by pressing Windows key + E.

Click Documents, located under 'This PC' or 'Quick access':

![FIle Explorer Documents](../images/file-explorer-docs.png)

Select ![My Games](../images/my-games-folder.png) followed by ![Rigs of Rods User Folder](../images/rigs-of-rods-folder.png). You are now in RoR's user directory.

Place the `*.zip` file inside the `mods` folder, either by cut (CTRL+X) and paste (CTRL+V) or drag and drop. Your mods folder should now have the zip inside:

![repository-install](../images/repository-installing-mod.png) 

You can also organize your mod zips by creating subfolders (e.g. `mods\cars\DodgeViperGTS.zip`).

That's it! You can launch Rigs of Rods now and your shiny new mod should be ready to use.

### Linux

For this, we'll be using Ubuntu 20.04. Instructions should be similar if you're using another distro.

First, click the ![Ubuntu Files Icon](../images/ubuntu-files-icon.png) icon located on your dock/launcher. You should now be in your Home directory. 

!!! warning
	If you installed RoR via the [Snap Store](https://snapcraft.io/rigs-of-rods), the user directory is located at `~/snap/rigs-of-rods/common/`.

By default, RoR's user folder is named `.rigsofrods`, which is a hidden folder. Hidden folders can be shown by clicking the top right menu icon and enabling 'Show Hidden Files':

![Ubuntu Show Hidden Files](../images/ubuntu-show-hf.png)

Once enabled, open the ![Ubuntu .rigsofrods Folder](../images/ubuntu-rigsofrods.png) folder. You are now in RoR's user directory.

Place the `*.zip` file inside the `mods` folder, either by cut (CTRL+X) and paste (CTRL+V) or drag and drop. Your mods folder should now have the zip inside: 

![Ubuntu Mod Installed](../images/ubuntu-installed-mod.png)

You can also organize your mod zips by creating subfolders (e.g. `mods\cars\DodgeViperGTS.zip`).

That's it! You can launch Rigs of Rods now and your shiny new mod should be ready to use.

## Where to download mods 

Mods can be downloaded from the official [Repository](https://forum.rigsofrods.org/resources/) and the [content](https://forum.rigsofrods.org/#showrooms.11) section of the forum. 
You should not download mods from unofficial sites, explained below.

## Things to avoid 

When it comes to installing RoR mods, there are some common mistakes new players make. Here's a list of things you should avoid when installing mods.

### Downloading mods from unofficial sources 

If you search for RoR mods on Google or YouTube, you'll likely find car mods that aren't available from the Repository. Almost all of these mods contain models ripped from other games/websites, which goes against our Terms of Service. 
They are not allowed on any of our services, including multiplayer. May also contain viruses and/or malware.

Further reading:<br>
[Don’t Steal Content or Violate Intellectual Property](../rules/community-guidelines.md#dont-steal-content-or-violate-intellectual-property)<br>
[Stolen Content (Bus Epidemic)](https://forum.rigsofrods.org/threads/stolen-content-bus-epidemic.2034/)

### Extracting zips 

Unless specified in the file description (e.g. a content pack) you should **NEVER** extract a mod zip! Extracting usually results in conflicts with other mods, and model/texture loading failures. 

### Installing mods in the game directory

Some new players who fail to read this page find RoR's install directory (where `RoR.exe` is) and end up placing mod zips in the `content` folder. 

This folder is **ONLY** for default content, installing mods here will likely result in them getting overwritten during an update or removed if you decide to uninstall. Please install mods in the correct directory, as explained above.

## Installing content packs 

To install content packs (a zip file containing multiple zips inside) such as the [Gabester Vehicle Pack](http://forum.rigsofrods.org/resources/gabester-vehicle-pack.12/) or the [content packs](https://forum.rigsofrods.org/resources/categories/content-packs.10/), just extract the zip (using File Explorer or 7-Zip) into the `mods` folder.

## Installing skinzips

Some mods may provide a `*.skinzip` which contains some extra liveries/skins for the vehicle. To install these, just place them inside the `mods` folder.

For more information about skinzips, see [this page](../vehicle-creation/alternate-skins.md).

## PSD/PDN files

These are files meant to be used by photo editing programs such as Photoshop or paint.net, they are not meant to be placed in the RoR directories.
