---
layout: page
title:  "Blender mesh editing"
categories: [tools-tutorials]
---

<div style="background-color:#FFFFCC; border: 1px solid #FFCC00; padding:0.2em; margin:1em 5em">
    <div style="float:left;"><a href="/images/NoticeIcon.png" class="image"><img alt="NoticeIcon.png" src="/images/NoticeIcon.png" width="32" height="32" /></a></div>
    <div style="margin-left:40px"><strong>Notice</strong><br />This tutorial assumes you have some basic knowledge on using Blender (Navigating UI, basic object editing, etc). There are plenty of tutorials available on YouTube or many other websites.</div>
</div>


<div class="toc" markdown="1">
  * TOC
  {:toc}
</div>

# Introduction 

Rigs of Rods is a game that is very easy to modify. This tutorial will help you get started on editing meshes using Blender, from installing the plug-ins to exporting.

# Required software

- [Blender](https://www.blender.org/download/) (2.79b is the latest at the time of writing)
- [Blender2ogre plug-in](/download/blender2ogre-0.6.0.zip)
- [Torchlight-To-Blender plug-in](/download/ImportExportTL_blender25x_v0.6.2.zip)
- (Optional) [Notepad++](https://notepad-plus-plus.org/)
- (Optional) [OgreCommandLineTools-Windows](https://sourceforge.net/projects/ogre/files/ogre-tools/1.7.2/OgreCommandLineTools_1.7.2.zip/download) (If you don't want to use the OgreXMLConverter located in your RoR install directory)
- (Optional) [OgreMeshy](https://sourceforge.net/projects/ogremeshy/)

# Getting started

If you're following this tutorial, chances are you probably already have a mesh you want to edit. In this tutorial I'll be editing Box5Diesel's Ram EXT.
Open the `.zip` file for the vehicle, and extract the correct `.mesh` file(s) and the textures (`.dds`, `.png`, etc) into a folder you can easily access:


![1](/images/blender-edit-meshandtextures.png)


Next you will need to convert the `.mesh` file into a `.mesh.xml` using OgreXMLConverter which can be found in your RoR install directory (Where `RoR.exe` is) or by downloading it from the link above. Just simply drag the mesh file into `OgreXMLConverter.exe`:

![2](/images/blender-edit-converting-mesh-to-xml.png)


If you're on Linux, you can use WINE to run `OgreXMLConverter.exe`by running this command in a terminal:
```
wine PATH/OgreXmlConverter.exe PATH/MESH_NAME.mesh
```

<div style="background-color:#FFFFCC; border: 1px solid #FFCC00; padding:0.2em; margin:1em 5em">
    <div style="float:left;"><a href="/images/NoticeIcon.png" class="image"><img alt="NoticeIcon.png" src="/images/NoticeIcon.png" width="32" height="32" /></a></div>
    <div style="margin-left:40px"><strong>Notice</strong><br />Some meshes are exported in OGRE 1.8 format, which only RoR 0.4+ supports. You'll have to use OgreXMLConverter from those versions. The OgreCommandLineTools download only supports OGRE 1.7.2.</div>
</div>

You should now have a `.mesh.xml` file in the same folder:


![3](/images/blender-edit-converted-xml.png)

We're ready to launch Blender now.

# Installing Blender plug-ins

First, download the two plug-ins from the links above and place them in any folder. **Do not extract.**

Now open Blender. Click `File` -> `User Preferences`:


![4](/images/blender-edit-userprefs1.png)

Click `Add-ons` -> `Install from File`:

![5](/images/blender-edit-userprefs2.png)

Select the `blender2ogre-0.6.0.zip` file you downloaded earlier. You should now see the Add-on installed, but it is not enabled yet. Click the check box to enable it:

![6](/images/blender-edit-userprefs3.png)

Now click `Install from File` again and select the `ImportExportTL_blender25x_v0.6.2.zip` file. Enable the add-on.

Once both plug-ins are enabled, select "Save User Settings":

![7](/images/blender-edit-userprefs4.png)

You can now close the `User Preferences` window. 

# Importing the mesh

Select `File` -> `Import` -> `Torchlight OGRE (.mesh)`:


![8](/images/blender-edit-import1.png)

Find & select the `.mesh` file. If you don't want it to delete the `.mesh.xml` file then select "Keep XML":

![9](/images/blender-edit-import2.png)

You should now see something similar to this:

![10](/images/blender-edit-justimported.png)

Press the `Z` key twice to get out of that shading mode. You should now see this:

![11](/images/blender-edit-zkeytwice.png)

<div style="background-color:#FFFFCC; border: 1px solid #FFCC00; padding:0.2em; margin:1em 5em">
    <div style="float:left;"><a href="/images/NoticeIcon.png" class="image"><img alt="NoticeIcon.png" src="/images/NoticeIcon.png" width="32" height="32" /></a></div>
    <div style="margin-left:40px"><strong>Notice</strong><br />The importer will automatically separate the meshes if the `.mesh.xml` contains multiple groups. The object names match the material name. If there's many objects with the same name, you should be safe to join them:
<br>
<a href="/images/blender-edit-joiningobjects.png" class="image"><img alt="blender-edit-joiningobjects.png" src="/images/blender-edit-joiningobjects.png" width="620" height="320" /></a>
</div>
</div>

It should look similar to this now:

![12](/images/blender-edit-objectsjoined.png)

# Fixing object shading

You'll probably notice that your mesh is very blocky/has lots of shading errors. To fix this:

On the left menu (Press `T` if it's not already open) select `Smooth`. You need to be in Object Mode (`TAB` key) for this to appear:

![13](/images/blender-edit-setsmooth.png)

Now press the `TAB` key again to go into Edit Mode:

![14](/images/blender-edit-editmode.png)

Select `Remove Doubles` from the `T` menu:

![15](/images/blender-edit-removingdoubles.png)

Now head over to the tool menu on the right and find the blue tool icon -> `Add Modifier` -> `Edge Split`:

![16](/images/blender-edit-edgesplit1.png)

The `Edge Split` Modifier should now be selected. The default `Split Angle` (30) should be fine in most cases. **Do not apply the modifier. The exporter will do this for you.**

![17](/images/blender-edit-edgesplit2.png)

# Applying the texture

Now we can apply the texture. Press the `TAB` key to go into Edit Mode if you're not in it already and click the circle icon on the bottom left -> `UV/Image Editor`:

![18](/images/blender-edit-applyingtexture1.png)

The `UV/Image Editor` should now be open:

![19](/images/blender-edit-applyingtexture2.png)

Select `Open` from the bottom bar:

![20](/images/blender-edit-applyingtexture3.png)

Find & select your texture file:

![21](/images/blender-edit-applyingtexture4.png)

The texture file should now be open in the `UV/Image Editor`. 

Now go to the top right and find the little plus icon, or press `N` to open it:

![22](/images/blender-edit-applyingtexture5.png)

Open the `Shading` menu and click `Textured Solid`:

![23](/images/blender-edit-applyingtexture6.png)


It should now look similar to this:

![24](/images/blender-edit-applyingtexture7.png)

# Editing the mesh

You're now ready to start editing the mesh. For this tutorial, I removed the stacks from the bed:

![25](/images/blender-edit-editedmesh.png)

# Setting the object name and material

Go to the right tool menu and select the triangle icon -> Change the name. This will be the name of your object when you export it:

![26](/images/blender-edit-naming-mesh.png)

Now select the circle icon next to the triangle icon -> `New`:

![27](/images/blender-edit-mat1.png)

To find your material name, either look at the object name or open the `.mesh.xml` file in a text editor and search "material":

![28](/images/blender-edit-finding-mat.png)

![29](/images/blender-edit-mat2.png)

# Exporting

Before we export, if you moved the object while editing it you will need to apply `Scale/Rotation/Location` by pressing `CTRL+A` otherwise it will be placed wrong in-game:

![30](/images/blender-edit-ctrla.png)

Select your mesh then click `File` -> `Export` -> `Ogre3D (.scene and .mesh)`:

![31](/images/blender-edit-export1.png)

Change your export settings to match the screenshot (all other settings can be left to their defaults):

![32](/images/blender-edit-export2.png)

You should now have a new `.mesh.xml` file in your folder.

And finally, just drag the `.mesh.xml` into OgreXMLConverter to get a `.mesh`:

![33](/images/blender-edit-converting-new-xml.png)

If you want to "preview" your `.mesh` instead of going in-game, you can use [Ogre Meshy](https://sourceforge.net/projects/ogremeshy/) to view it:
(You can make a `.material` file if you want it to be textured in Ogre Meshy)

![35](/images/blender-edit-preview-ogremeshtool.png)

# Testing in-game

Now just edit the `.truck` file to match the name of your new mesh and drag the new mesh file back into the `.zip` and test in-game:

![35](/images/blender-edit-ingame.png)

Congratulations!


# Troubleshooting

**Q:** My mesh is flipped in-game!

**A:** Change the "swap axis" option in the export settings.

---------------------------------------

**Q:** My mesh is white in-game!

**A:** You did not assign the correct material. Make sure it matches.

---------------------------------------

**Q:**: I get a plug-in install error/other Blender errors!

**A:**: First, just Google the issue. If you can't find a solution then you can create a thread on the [content creation forum](https://forum.rigsofrods.org/forums/content-creation.15/).


---------------------------------------
