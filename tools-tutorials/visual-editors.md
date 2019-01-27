---
layout: page
title:  "Visual editors"
categories: [tools-tutorials]
---

<div class="toc" markdown="1">
  * TOC
  {:toc}
</div>

# Introduction

While it is possible to create a node/beam completely using a text editor, it is not recommended as an n/b can get quite complex. 

These are programs that help you visualize and edit a node/beam.

# Truck file template

To help you get started with creating a new node/beam, you can download this truck file template which contains all the required sections.

[Blank Truck File](https://forum.rigsofrods.org/content-creation/15-blank-truck-file.html)

# Editorizer

![Editorizer](/images/editorizer.png)


Arguably the most popular editor, the Editorizer is a free program written by Ben for making vehicles. Contributions: Tuusita (Comments, Structure, Connect To).

It's a fairly old and simple program. Note you can't use it to create a new vehicle from scratch, you need to manually create a _.truck_ file with a basic structure. A  _.truck_ file with the basic structure has been included to get you started.

Pros:
- Designed for editing node/beam, very feature-rich
- Colors can be changed to suit your liking

Cons:
- Does not support newer `.truck` sections (such as `set_node_defaults`). These sections will have to be commented out otherwise the Editorizer fails to open the file.

It is recommended to make a copy of the truck file made for editing, then copy the changes over to your main truck file.

## Download and run on Windows

[Download here](https://forum.rigsofrods.org/resources/editorizer.20/) (ZIP archive)

Run as administrator! (only needed on the first run or if you move Editorizer's directory)

### Troubleshooting

If you don't run Editorizer as administrator for the first time, or you subsequently move it's directory, you may encounter this error:
![](/images/editorizer-error-comdlg32ocx.jpeg)

To resolve this, try running as administrator again, and if it doesn't help, try these steps:

-   Find comdlg32.ocx and mscomctl.ocx in Editorizer's directory.
-   On 32-bit Windows:
    -   Move comdlg32.ocx and mscomctl.ocx to _C:\\Windows\\system32_.
    -   Open a command line window and run following commands:
    
        ```
        regsvr32 c:\Windows\system32\comdlg32.ocx
        regsvr32 c:\Windows\system32\mscomctl.ocx
        ```
-   On 64bit Windows:
    -   Move comdlg32.ocx and mscomctl.ocx to _C:\\Windows\\SysWOW64_
    -   Open a command line window and run following commands:
    
        ```
        regsvr32 c:\Windows\SysWOW64\comdlg32.ocx
        regsvr32 c:\Windows\SysWOW64\mscomctl.ocx
        ```

## Download and run on MacOSX

[Download here](http://www.mediafire.com/download/ji2edf2ng4rcy9b/MAC%20RoR%20Editorizer.zip) (ZIP archive)

Requires MacOSX Snow Leopard or Higher.

The mac port is standalone with all the files needed built into the app, Huge thanks to MothBird.

Warning: the file is quite large (511.6MB) because of all of the required frameworks.


## Using blueprints

Blueprints are technical drawings of vehicles and machinery, very useful as reference. Many good blueprints can be found on the internet.

To load a blueprint, find _Blueprints_ in the top toolbar, and load in the files.

To adjust blueprints, click on _Place Blueprints_ on the far right, and place your blueprints in a desired position .

## Editing Nodes

When you want to add nodes, just click on _Add Nodes_ up in the right. Click where you want the node to go, either in the Top Left, Bottom Left or Botton Right areas. If you want to make the node only get placed on the "grid" that divides the areas up-check the "snap nodes to grid" box.
Special Nodes

Check [truckfile reference](technical/fileformat-truck) for special node types.

If you want to give your nodes these special options, just click on the _Nodes_ tab, pick the one you want to change, and put the corresponding node option in the options part.

## Editing Beams

When you want to add beams, just click on the _Add Beams_ up in the right. Click the first node where you want the beam to start. Click the second node which is where you want the beam to end.

Check [truckfile reference](technical/fileformat-truck) for special beam types.

If you want to give your beams these special options, just click on the _Beams_ tab, pick the beam you want to change, and put the corresponding beam option in the options box, along with any variables for that type of beam.

## Wheels

To add wheels, look at this example. Just click on the Wheels tab and add in the correct information in the correct spaces.

FRONT WHEELS(Steering wheels):

```
wheels
; EXAMPLE: 
0.5,0.1,12,33,34,9999,1,1,32,350.0,300000,4000, tracks/wheelface tracks/wheelband1
; EXAMPLE2: 
0.5,0.1,12,35,36,9999,1,1,31,350.0,300000,4000, tracks/wheelface tracks/wheelband1 
```

REAR WHEELS:

```
wheels
;EXAMPLE: 
0.5,0.1,12,12,13,14,1,1,10,350.0,300000,4000, tracks/wheelfaceb tracks/wheelband1
;EXAMPLE2: 
0.5,0.1,12,14,15,-12,1,1,9,350.0,300000,4000, tracks/wheelfaceb tracks/wheelband1 
```

## Scaling

To scale your vehicle if you find it a little bit too big, just go to the Visible Nodes tab at the very top. Click on Scale..., then put in decimal numbers from 0.01 to 0.99 in the X,Y,Z lines to scale it down, put in decimal numbers from 1.0 and up(experiment) to scale it up.

## Tools to avoid

In the _Visible Nodes_ tab at the top, I would advise to not use the _Interconnect_ or _Variable Interconnect_ options with any vehicle as it can mess up the structure and other things. Basically these options will join every node to every other node in the object... 

# Blender 2.49b

Sometimes used in combination with the Editorizer, this very old version of Blender includes plugins for importing/exporting truck files.

![blender249b](/images/blender_249b.png)

Pros:
- Easily create/edit nodes and beams 
- Create and UV map submesh 
- Can import a 3d model to help you shape your node/beam.

Cons:
- Only displays nodes/beams/shocks. 
- As it is an old version, the UI and controls are vastly different from the latest Blender version. It is possible to build the node/beam in the latest Blender, then open it in 2.49b to export to a `.truck` file.
- Beams that are connected to non-existant nodes (e.g. beams attached to wheel nodes) will have to be commented out as Blender will fail to import the file.

It is recommended to export to a copy of the truck file made for editing, then copy the changes over to your main truck file.

## Download

[Download here](http://www.austingratzer.com/rigs/downloads.php?do=file&id=180) (Windows only)

# TruckViewer

A Java program made by Gouranga designed for viewing a node/beam structure.

![truckviewer](/images/truckviewer.png)

Pros:
- Auto-reloading of the file
- Supports nodes2
- 4 independent views, each can be either be rotated in 3d or snapped to the front/sides/back.

Cons:
- Only displays pure nodes and beams.
- Cannot edit the n/b structure, it is designed only for viewing it.

## Download 

[Download here](https://forum.rigsofrods.org/resources/truckviewer.19/)

