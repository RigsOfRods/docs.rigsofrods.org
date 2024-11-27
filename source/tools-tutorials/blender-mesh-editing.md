Blender (2.7) mesh editing
============

## Introduction 

Rigs of Rods is a game that is very easy to modify. This tutorial will help you get started on editing meshes using Blender, from installing the add-ons to exporting.

We assume you already have some basic knowledge on using Blender (navigating UI, basic object editing, etc). There are plenty of tutorials available on YouTube or many other websites.

We'll also assume you are running Windows, however these instructions should mostly apply to Linux users.

**Please read everything carefully and do not skip any steps.**

!!! note "Disclaimer"
	This page's purpose is not to teach you how to make content from scratch, nor is it meant to discourage anyone from doing so. It is simply for those who are interested in editing existing models.
	Editing existing content is the easiest way to learn how RoR's content creation works, and this page is meant to help you get started. We currently do not have a tutorial on how to make a mod from scratch.

## Required software

- Rigs of Rods
- [Blender 2.79](https://download.blender.org/release/Blender2.79/)
- [Ogre Import/Export add-ons](https://github.com/CuriousMike56/RoROgreAddons)
- [Ogre Command Line Tools](https://forum.rigsofrods.org/resources/ogre-command-line-tools.967/)
- (Optional) [Notepad++](https://notepad-plus-plus.org/)
- (Optional) [OgreMeshy](https://forum.rigsofrods.org/resources/ogremeshy.595/)
- A brain, some basic computer knowledge, and some patience

## Blender version warning 

This page was written for Blender 2.79 and has not yet been updated for newer versions. For 2.8+ you can use the [blender2ogre plugin](https://github.com/OGRECave/blender2ogre) to import/export meshes.

When downloading Blender from the above link, avoid the versions in the `latest` folder! They do not support the addons. If you're unsure, download `blender-2.79-windows64.msi`.

## Getting started

If you're following this tutorial, chances are you probably already have a mesh you want to edit. In this tutorial I'll be editing [Box5Diesel's Ram EXT](https://forum.rigsofrods.org/resources/box-dodge-ram.319/).
Open the `.zip` file for the vehicle, and extract the correct `.mesh` file(s) and the textures (`.dds`, `.png`, etc) into a folder you can easily access:

![1](../images/blender-edit-meshandtextures.png)

Next, download the [Ogre Command Line Tools](https://forum.rigsofrods.org/resources/ogre-command-line-tools.967/) and extract the archive into a new folder. Inside you'll find `OgreXMLConverter.exe`.

Now simply drag and drop the mesh onto `OgreXMLConverter.exe` to get a `.mesh.xml`:

![2](../images/blender-edit-converting-mesh-to-xml.png)

You should now have a `.mesh.xml` file in the same folder:

![3](../images/blender-edit-converted-xml.png)

We're ready to launch Blender now.

## Installing Blender add-ons

First, download the latest [Ogre Import/Export add-ons](https://github.com/CuriousMike56/RoROgreAddons/releases) from GitHub (`RoR_ImportExport_*.zip`) and place it into any folder. **Do not extract.**

Now open Blender. Click `File` -> `User Preferences`:

![4](../images/blender-edit-userprefs1.png)

Click `Add-ons` -> `Install from File`:

![5](../images/blender-edit-userprefs2.png)

Select the `RoR_ImportExport_*.zip` file you downloaded earlier.

Type `rigs` into the search bar and both add-ons should appear:

![6](../images/blender-edit-userprefs3.png)

Once both add-ons are enabled by clicking the checkbox, select `Save User Settings`:

![7](../images/blender-edit-userprefs4.png)

You can now close the `User Preferences` window. 

## Importing the mesh

Select `File` -> `Import` -> `Ogre3D (.mesh.xml)`:

![8](../images/blender-edit-import1.png)

Find & select the `.mesh` file.

![9](../images/blender-edit-import2.png)

You should now see something similar to this:

![10](../images/blender-edit-justimported.png)

Press the `Z` key twice to get out of that shading mode. You should now see this:

![11](../images/blender-edit-zkeytwice.png)

!!! warning
    The importer will automatically separate meshes if the `.mesh.xml` contains multiple materials. The object names match the material name. If there's many objects with the same material name, you should be safe to join them by pressing `CTRL+J`:
	
    ![blender-edit-joiningobjects.png](../images/blender-edit-joiningobjects.png)


It should look similar to this now:

![12](../images/blender-edit-objectsjoined.png)

## Fixing object shading

You'll probably notice that your mesh is very blocky and/or has lots of shading errors. To fix this:

On the left menu (Press `T` if it's not already open) select `Smooth`. You need to be in Object Mode (`TAB` key) for this to appear:

![13](../images/blender-edit-setsmooth.png)

Now press the `TAB` key again to go into Edit Mode:

![14](../images/blender-edit-editmode.png)

Select `Remove Doubles` from the `T` menu:

![15](../images/blender-edit-removingdoubles.png)

Now head over to the tool menu on the right and find the blue wrench icon -> `Add Modifier` -> `Edge Split`:

![16](../images/blender-edit-edgesplit1.png)

The `Edge Split` Modifier should now be selected. The default `Split Angle` (30) should be fine in most cases. **Do not apply the modifier. The exporter will do this for you.**

![17](../images/blender-edit-edgesplit2.png)

!!! note
	For some models just applying edge split won't be enough, further work may be required (such as marking faces sharp).**

## Applying the texture

Now we can apply the texture. Press the `TAB` key to go into Edit Mode if you're not in it already and click the circle icon on the bottom left -> `UV/Image Editor`:

![18](../images/blender-edit-applyingtexture1.png)

The `UV/Image Editor` should now be open:

![19](../images/blender-edit-applyingtexture2.png)

Select `Open` from the bottom bar:

![20](../images/blender-edit-applyingtexture3.png)

Find & select your texture file:

![21](../images/blender-edit-applyingtexture4.png)

The texture file should now be open in the `UV/Image Editor`. 

Now go to the top right and find the little plus icon, or press `N` to open it:

![22](../images/blender-edit-applyingtexture5.png)

Open the `Shading` menu and click `Textured Solid`:

![23](../images/blender-edit-applyingtexture6.png)


It should now look similar to this:

![24](../images/blender-edit-applyingtexture7.png)

## Editing the mesh

You're now ready to start editing the mesh. For this tutorial, I removed the exhaust stacks from the bed:

![25](../images/blender-edit-editedmesh.png)

## Setting the object name

In the outliner (object list), double-click the object name to rename it. This will be the name of your mesh when exporting.

![26](../images/blender-edit-naming-mesh2.png)

In this example, I'll name it `BoxDodgeCummins-NoStacks`.

## Adding a material

Now select the circle icon next to the triangle icon and click `New`:

![27](../images/blender-edit-mat1.png)

The easiest way to find the material name is by opening the `.mesh.xml` file in a text editor and search "material":

![28](../images/blender-edit-finding-mat.png)

![29](../images/blender-edit-mat2.png)

## Exporting

Before we export, if you moved the object while editing it you will need to apply `Location/Rotation/Scale` by pressing `CTRL+A` otherwise it will be placed incorrectly in-game:

![30](../images/blender-edit-ctrla.png)

Select your mesh then click `File` -> `Export` -> `Ogre3D (.scene and .mesh.xml)`:

![31](../images/blender-edit-export1.png)

Change your export settings to match the screenshot (all other settings can be left to their defaults):

![32](../images/blender-edit-export2.png)

You should now have a new `.mesh.xml` and `.mesh` file in your folder:

![32.1](../images/blender-edit-exported.png)

The exporter will automatically convert the `.mesh.xml` to `.mesh` as long RoR is installed to the default location.

If you want to preview your exported model, you can use [OgreMeshy](https://forum.rigsofrods.org/resources/ogremeshy.595/) to view it:
(You can make a `.material` file if you want it to be textured in OgreMeshy)

![35](../images/blender-edit-preview-ogremeshtool.png)

## Testing in-game

Now just edit the vehicle's `.truck` file to match the name of your new mesh and drag the new mesh file back into the `.zip` and test in-game:

```
17,14,2, 0.73, 0.5, 0.07, 0, 0, 0, BoxDodgeCummins-NoStacks.mesh
forset 7, 12, 40, 41, 44-66, 69-87, 111
```

![35](../images/blender-edit-ingame.png)

Congratulations!

## Troubleshooting

#### [Error 2] No such file or directory

You forgot to convert the `.mesh` to `.mesh.xml`, as described in the [Getting started](#getting-started) section.

!!! warning
	On Linux there is currently a bug preventing `.mesh.xml` imports in uppercase paths (e.g. `/home/user/Downloads/rorimportfiles`. You will have to place the `.mesh` and `.mesh.xml` files into a different folder without uppercases (e.g. `/home/user/rorimportfiles`)

#### Mesh is rotated incorrectly

Change the "swap axis" option in the export settings:

![36](../images/blender-export-swap-axis.png)

Rigs of Rods meshes require the axis to be swapped to `xz-y` due to differences in the axises between RoR and Blender:

In RoR x is front-back, y is up-down, z is side to side

In Blender x is side to side, z is up-down, y is front-back

#### Mesh appears white/black/pink

You did not assign the correct material or you named it incorrectly. Make sure it matches.

White/pink means the game can't find the material, while black means the game found the material but not the texture. 
You can search the mesh name in your RoR.log to find the error. 

#### Other errors

If you're experiencing issues, you can create a thread on the [content creation forum](https://forum.rigsofrods.org/forums/content-creation.15/) or join the [RoR Discord](https://discord.gg/rigsofrods) and ask in the #modding channel.