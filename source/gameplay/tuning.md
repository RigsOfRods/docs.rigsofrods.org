Tuning
============

!!! warning
	This feature is in development. It will be made available in an upcoming release. If you're interested in trying this out today, download the latest [development build](https://forum.rigsofrods.org/threads/ror-development-builds-for-windows-and-linux.696/).

## Introduction

The tuning menu is a new single player feature available for vehicles. It enables the ability to install add-on parts, toggle visibility of meshes and visual effects, flip wheel direction, and save/load tuneups.

Tuning is currently disabled in Multiplayer, support will be added in a future release.

For a technical overview of the addonpart file format, see: [Addonpart file format](/vehicle-creation/fileformat-addonpart)

<img src="/images/tuning-menu.png" width="400">

## Addon parts

The main feature of the Tuning menu is the ability to install add-on parts with one click, without manually editing the [truck file](/vehicle-creation/fileformat-truck/).

Add-ons for the currently spawned vehicle will be displayed. Add-ons can be downloaded from the in-game Repository or the [website](https://forum.rigsofrods.org/resources/categories/addons.15/) and placed into the `mods` folder just like vehicles and terrains.
Please note that only a handful of parts currently support the new file format. 

To install a part, simply click the box next to the part name. Click again to remove.

### Part conflicts

When hovering over an add-on part, red outlines around other parts may appear:

![addon-part-conflicts](/images/addon-part-conflicts.png)

These are conflicts. Conflicting parts cannot be installed together. When installing a part that conflicts, the other parts will be disabled (marked with an X).

Attempting to install a conflicting part through the selector will display an error:

![addon-part-conflict2](/images/addon-part-conflict2.png)

### Parts selector

Below the parts list is a `Browse all parts` button. The parts selector displays all installed addonparts:

<img src="/images/parts-menu.png" width="900">

From this menu it's possible to force install any part. **Keep in mind that most parts are designed for specific vehicles, installing them will likely result in glitches or other unexpected behavior!**

The main exception to this are wheels. Some wheels (such as the [StanceWerkz Wheel Pack](https://forum.rigsofrods.org/resources/stancewerkz-wheel-pack.1151/)) are designed to be installed onto most vehicles. 
These wheels can only be installed through the parts selector.

## Visual elements

The Tuning menu also features the ability to toggle the visibility of props, flexbodies, flares (lights), exhaust smoke, and managedmaterials:

<img src="/images/tuning-meshlist.png" width="800">

![tuning-flexbody-toggle](/images/tuning-flexbody-toggle.gif)

Numbers next to element names are IDs, these are used for the [addonpart file format](/vehicle-creation/fileformat-addonpart/).

Disabled elements are moved to the bottom of the list. 

### Protected 

With the "Protected" option, it's possible to 'lock' an element from being changed or disabled by an add-on part.
This can be useful for disabling specific elements of an addon (for instance, parts of a body kit).

## Wheels

When installing wheel addons, it's possible for the wheel mesh to be facing the wrong direction. This can be fixed through the Tuning menu:

![tuning-wheelside](/images/tuning-wheelside.png)

Some vehicles feature flexbody tires, if the wheel includes a pre-mounted tire you will need to hide them:

![tuning-hide-flextires](/images/tuning-hide-flextires.png)

## Saving and loading

Once you're finished customizing a vehicle, it can be saved by clicking `Save as...` at the top of the Tuning menu:

!!! note 
	The `Save as...` button only appears after installing an add-on or toggling an element. 

![tuning-save1](/images/tuning-save1.png)

Give it a name, then click `Save`. Existing tunes with the same name will not be overwritten unless `Overwrite` is enabled.

![tuning-save2](/images/tuning-save2.png)

![tuning-save3](/images/tuning-save3.png)

The tune is now saved. Simply click on the tune name to load it. Press & hold the `Delete` button to permanently remove a tune.

Tunes are saved in `.tuneup` files inside a new `projects` folder in the user directory.

### Savegames

Savegames work seamlessly with Tuning, any changes you make to spawned vehicles will be saved. 

When loading a savegame, the game may freeze/hang for a second when accessing the Tuning menu. This is caused by the conflict check and is normal.
