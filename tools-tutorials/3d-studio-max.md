---
layout: page
title:  "3D Studio Max"
categories: [tools-tutorials]
---

<div class="toc" markdown="1">
  * TOC
  {:toc}
</div>

# Intro

**3ds Max** is a professional 3D modeling, animation, and rendering package from 
[http://www.autodesk.com/ Autodesk]. 
You can use it to build and skin meshes for RoR. 
Get more information on 3ds Max [http://usa.autodesk.com/3ds-max/ here]. 
You can export your meshes and materials using [http://www.ogremax.com/ OgreMax Scene Exporter]. 
There is also an old importer/exporter (described below) available which lets you import/export RoR-files in 3ds Max. 
You can also use this to build your node and beam structure.

# importer/exporter tool

These are a set of scripts which allow RoR trucks to be edited within 3ds Max. 
These scripts don't work in 3ds Max 2013!

## Features

The ultimate goal of these tools would be to give the user the ability 
to edit absolutely any part of a truck, so that they would never, 
ever have to use a text editor to make changes to a truck. 
Although this probably cannot be fully achieved, due to a number 
of restrictions with 3ds Max, the scripts have been with this 'philosophy' in mind. 

One of the biggest advantages of these scripts is that there is no need to use node numbers 
when editing trucks: everything is done by object positions. 

## List of fully supported sections

The following truck file sections are fully supported by the scripts:

    | author || commands2 || fixes || importcommands || ropes
    | axle rigidity nodes || contacters || forwardcommands || meshwheels || set_skeleton_settings
    | beams || description || friction nodes || minimass || shocks
    | brakes || engine || globals || nodes || submesh
    | buoyancy nodes || engoption || globeams || non contact nodes || terrain nodes
    | camera nodes || exhaust X nodes || guisettings || reference arm nodes || ties
    | cameras || exhaust Y nodes || help || rigidifiers || title
    | cinecam || exhausts || hook nodes || rollon || wheels
    | commands || fileinfo || hydros || ropables || wheels2

## Installation and compatibility 

Download [http://modclub.rigsofrods.com/tommylommykins/RoRTools.zip this] zip 
file and extract the entire package into the scripts directory of your copy of 3ds max. 
An example location would be "C:\Program Files\Autodesk\3ds Max 9\Scripts\RoRTools" 

The tools will work with 3ds Max version 9 and above. 

## Quick Start  

There are 5 scripts in the package, you will only ever need to use three. 
they are "RoRImporter.ms" (for importing trucks into 3dsm), "RorExporter.3ds" 
(For exporting trucks out of 3dsm), and "editor.ms" (for opening the editor dialogue) 

## Running the scripts  

### Importer 

<a href="/images/tools-3dsmax-importexport01-runscript.png">
 <img src="/images/tools-3dsmax-importexport01-runscript.png">
 <br>The 'run script' menu option in 3dsm
</a>

<a href="/images/tools-3dsmax-importexport02-truck.png">
 <img src="/images/tools-3dsmax-importexport02-truck.png">
 <br>The wrecker, as it appears after import in 3dsm
</a>

To import a truck, click on the "maxscript" menu button in the toolbar and then click on "Run Script." 
An open file dialog will appear with the title "choose editor file". 
Open RoRImporter.ms. Another open file dialog will appear, with the title "Open". 
Select the truck you want to import with this dialog, and the truck will be imported.

### Exporter  

Run RoRExporter.ms to export a truck. Unlike all the other editors for RoR trucks, 
the exporter will always write a completely new truck file when exporting: 
None of the data in a truck that you might be overwriting will be kept.

### Editor  

<a href="/images/tools-3dsmax-importexport03-data.png">
 <img src="/images/tools-3dsmax-importexport03-data.png">
 <br>the data editor
</a>

the data editor can be accessed by running "editor.ms" in 3dsm, which places it 
in the utilities tab. It must be used to create all RoR objects, 
failure to do so will result in an incomplete export. 

## Detailed description 

the most important objects for 3dsm are the beam objects, since they are the only objects which can define nodes. No other objects, such as hydros, wheels, shocks can define nodes (ropes are an exception to this). When exporting these non-node-defining objects, their node references are created by finding the nearest corner of the beams and using its node. 

## Editing trucks in 3ds  

All objects (such as shocks, beams, hydros, etc) must be created in using the Data editor ("editor.ms"). 

Objects can largely be broken into a few small categories: 

* Beam-objects (wheels, shocks, hydros, etc.) 
* Node-reference objects (node flags, rigidifiers, etc.) 
* Submesh-objects (submeshes)

3ds can only tell which object is which from the name of each object. usually, the first part of the object's nameis used to define things. Beams are in the format "beam_ABCXYZ", wheels are in the format "wheel_ABCXYZ" and shocks are in the format "shock_ABCXYZ". Not using a recognised format for an object, or changing the name of an object after creation (ie. changing "beam_1" to "xbeam_1") will result in it not being exported. 

## Beam-objects

With the exception of beams themselves, objects are made up on only one spline segment (beams can have many spline segments). These generally represent the special beams in RoR which are coloured white. 

To modify beam objects choose them, go to vertex mode and move the corresponding nodes where you want them. To add a new beam use the "create beam" button in the editor.ms. Activate "snap on vertex", click on the first node and drag to the second, the beam will be created.

## Node-reference objects

To create node-reference-objects, go to vertex mode and choose the nodes where you want the object to be created. Now go to the editor.ms panel and choose the type of object you want. It will be displayed as a small cube. 

## Submesh-objects

<a href="/images/tools-3dsmax-importexport04-truck.png">
 <img src="/images/tools-3dsmax-importexport04-truck.png">
 <br>The standard wrecker, with a material containing its normal texture file in 3ds
</a>

Submeshes are displayed as standard editable meshes in 3ds, separated by smoothing group. They do not have a texture applied on import, but a material can be applied with the truck's normal texture if the image needs to be displayed on the truck for UVW editing. To add a new submesh use the "add submesh" button in the editor.ms. Activate "snap on vertex" and draw the submesh.

## Building mods completely with 3ds Max 
It is also possible to build a new mod completely in 3ds Max. A possible workflow:

Step 1: Build the meshes (props/flexbodies) for your mod

Step 2: Build a very basic shape of your vehicle in polygon modeling, this will be the base of your node and beam structure

Step 3: Go to edge selection mode and select all edges of your poly

Step 4: Right-click on and select "create shape", choose linear and a name beginning with ""beam_...", now you have a very basic node and beam structure

Step 5: Do not delete your poly, you can use it for collision! convert it to a mesh and rename it to "submesh_..."

Step 6: Now you can add support beams to your n&b using the "create line" tool and snap on vertex

Step 7: Run the editor.ms maxscript and add the things you want, i.e. commands, hydros, ...

Step 8: Export your model to a truck file using the rorexporter.ms maxscript

Step 9: Export your props/flexbodies using the Ogremax exporter [http://www.ogremax.com/]. A tip for a much easier prop and flexbody placing: Choose "adjust turning point" in the hirachy menu and move the gizmo to the node where the mesh should be placed. Uncheck "adjust turning point" and move your mesh to 0, 0, 0. Now export the mesh, it is now perfectly aligned to it's destination node. There is no need to play with the offset values any more, only the rotation values have to be adjusted.

Step 10: Use the Node Renumbering Tool to arrange the node numbers the way you want them.

Step 11: Now you can tweak your mod in your text editor.
