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

**Please read everything carefully and do not skip any steps.**

**If you've created a model yourself and just want to export it to RoR, skip to the [Exporting](#exporting) section.**

# Required software

- Rigs of Rods installed to the default location (`C:\Program Files\Rigs of Rods`)
- [Blender](https://www.blender.org/download/previous-versions/) (2.79b)
- [Ogre Import/Export plug-ins](/download/OGRE_ImportExport_RoR.zip)
- (Optional) [Notepad++](https://notepad-plus-plus.org/)
- (Optional) [OgreMeshy](https://sourceforge.net/projects/ogremeshy/)
- A brain, some basic computer knowledge, and some patience

# Blender version warning 

The latest version of Blender (2.80) is currently not supported as the plugins have not been updated for it yet. You can download 2.79b [here](https://download.blender.org/release/Blender2.79/).

If you are unsure which file to download, just select `blender-2.79b-windows64.zip ` and extract it into a new folder, then run `blender.exe`.

# Getting started

If you're following this tutorial, chances are you probably already have a mesh you want to edit. In this tutorial I'll be editing Box5Diesel's Ram EXT.
Open the `.zip` file for the vehicle, and extract the correct `.mesh` file(s) and the textures (`.dds`, `.png`, etc) into a folder you can easily access:


![1](/images/blender-edit-meshandtextures.png)

Next, open a new File Explorer window and browse to `C:\Program Files\Rigs of Rods`, this is where `OgreXMLConverter.exe` is located. 

Simply drag and drop the mesh onto `OgreXMLConverter.exe` to get a `.mesh.xml`:

![2](/images/blender-edit-converting-mesh-to-xml.png)

You should now have a `.mesh.xml` file in the same folder:

![3](/images/blender-edit-converted-xml.png)

We're ready to launch Blender now.

# Installing Blender plug-ins

First, download the [Ogre Import/Export plug-ins](/download/OGRE_ImportExport_RoR.zip) and place it into any folder. **Do not extract.**

Now open Blender. Click `File` -> `User Preferences`:

![4](/images/blender-edit-userprefs1.png)

Click `Add-ons` -> `Install from File`:

![5](/images/blender-edit-userprefs2.png)

Select the `OGRE_ImportExport_RoR.zip` file you downloaded earlier.

Type `rigs` into the search bar and both add-ons should appear:

![6](/images/blender-edit-userprefs3.png)

Once both plug-ins are enabled by clicking the checkbox, select `Save User Settings`:

![7](/images/blender-edit-userprefs4.png)

You can now close the `User Preferences` window. 

# Importing the mesh

Select `File` -> `Import` -> `Ogre3D (.mesh.xml)`:

![8](/images/blender-edit-import1.png)

Find & select the `.mesh` file.

![9](/images/blender-edit-import2.png)

You should now see something similar to this:

![10](/images/blender-edit-justimported.png)

Press the `Z` key twice to get out of that shading mode. You should now see this:

![11](/images/blender-edit-zkeytwice.png)

<div style="background-color:#FFFFCC; border: 1px solid #FFCC00; padding:0.2em; margin:1em 5em">
    <div style="float:left;"><a href="/images/NoticeIcon.png" class="image"><img alt="NoticeIcon.png" src="/images/NoticeIcon.png" width="32" height="32" /></a></div>
    <div style="margin-left:40px"><strong>Notice</strong><br />The importer will automatically separate meshes if the `.mesh.xml` contains multiple materials. The object names match the material name. If there's many objects with the same material name, you should be safe to join them by pressing `CTRL+J`:
<br>
<a href="/images/blender-edit-joiningobjects.png" class="image"><img alt="blender-edit-joiningobjects.png" src="/images/blender-edit-joiningobjects.png" width="620" height="320" /></a>
</div>
</div>

It should look similar to this now:

![12](/images/blender-edit-objectsjoined.png)

# Fixing object shading

You'll probably notice that your mesh is very blocky and/or has lots of shading errors. To fix this:

On the left menu (Press `T` if it's not already open) select `Smooth`. You need to be in Object Mode (`TAB` key) for this to appear:

![13](/images/blender-edit-setsmooth.png)

Now press the `TAB` key again to go into Edit Mode:

![14](/images/blender-edit-editmode.png)

Select `Remove Doubles` from the `T` menu:

![15](/images/blender-edit-removingdoubles.png)

Now head over to the tool menu on the right and find the blue wrench icon -> `Add Modifier` -> `Edge Split`:

![16](/images/blender-edit-edgesplit1.png)

The `Edge Split` Modifier should now be selected. The default `Split Angle` (30) should be fine in most cases. **Do not apply the modifier. The exporter will do this for you.**

![17](/images/blender-edit-edgesplit2.png)

**Note: For some models just applying edge split won't be enough, further work may be required (such as marking faces sharp).**

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

You're now ready to start editing the mesh. For this tutorial, I removed the exhaust stacks from the bed:

![25](/images/blender-edit-editedmesh.png)

# Setting the object name

Go to the right tool menu and select the triangle icon, then change the name in the box. This will be the name of your object when you export it:

![26](/images/blender-edit-naming-mesh.png)

In this example, I'll name it `BoxDodgeCummins-NoStacks`.

# Adding a material

Now select the circle icon next to the triangle icon and click `New`:

![27](/images/blender-edit-mat1.png)

In most cases your material name is the one shown in the object tree:

![27.1](/images/blender-edit-mat1.2.png)

You can also open the `.mesh.xml` file in a text editor and search "material":

![28](/images/blender-edit-finding-mat.png)

![29](/images/blender-edit-mat2.png)

# Exporting

Before we export, if you moved the object while editing it you will need to apply `Location/Rotation/Scale` by pressing `CTRL+A` otherwise it will be placed incorrectly in-game:

![30](/images/blender-edit-ctrla.png)

Select your mesh then click `File` -> `Export` -> `Ogre3D (.scene and .mesh.xml)`:

![31](/images/blender-edit-export1.png)

Change your export settings to match the screenshot (all other settings can be left to their defaults):

![32](/images/blender-edit-export2.png)

You should now have a new `.mesh.xml` and `.mesh` file in your folder:

![32.1](/images/blender-edit-exported.png)

The exporter will automatically convert the `.mesh.xml` to `.mesh` as long RoR is installed to the default location.

If you want to preview your exported model, you can use [Ogre Meshy](https://sourceforge.net/projects/ogremeshy/) to view it:
(You can make a `.material` file if you want it to be textured in Ogre Meshy)

![35](/images/blender-edit-preview-ogremeshtool.png)

# Testing in-game

Now just edit the vehicle's `.truck` file to match the name of your new mesh and drag the new mesh file back into the `.zip` and test in-game:

```
17,14,2, 0.73, 0.5, 0.07, 0, 0, 0, BoxDodgeCummins-NoStacks.mesh
forset 7, 12, 40, 41, 44-66, 69-87, 111
```

![35](/images/blender-edit-ingame.png)

Congratulations!

# Troubleshooting

### [Error 2] No such file or directory

You forgot to convert the `.mesh` to `.mesh.xml`.

### Mesh is flipped

Change the "swap axis" option in the export settings.

### Mesh appears white/pink

You did not assign the correct material. Make sure it matches.

### Other errors

First, just Google the issue. If you can't find a solution then you can create a thread on the [content creation forum](https://forum.rigsofrods.org/forums/content-creation.15/).