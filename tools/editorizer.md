---
layout: page
title:  "Editorizer"
categories: [tools]
---

<div class="toc" markdown="1">
  * TOC
  {:toc}
</div>

The Editorizer is a free program written by Ben for making vehicles. Contributions: Tuusita (Comments, Structure, Connect To).

It's a fairly old and simple program. Note you can't use it to create a new vehicle from scratch, you need to manually create a _.truck_ file with a basic structure. The file must contain a section for nodes, beams, hydros, commands, shocks, and wheels. It can be blank to begin with or when saving but the heading must be there.

# Download and run on Windows

[Download here](https://repofiles.avrintech.net/repofiles-1st-batch/57ddb080d4ea83b7d40df778c916a66a379d4dd1_Editozer.zip) (ZIP archive)

Run as administrator! (only needed on the first run or if you move Editorizer's directory)

## Troubleshooting

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

# Download and run on MacOSX

[Download here](http://www.mediafire.com/download/ji2edf2ng4rcy9b/MAC%20RoR%20Editorizer.zip) (ZIP archive)

Requires MacOSX Snow Leopard or Higher.

The mac port is standalone with all the files needed built into the app, Huge thanks to MothBird.

Warning: the file is quite large (511.6MB) because of all of the required frameworks.

# Truck file template

Editorizer loads and saves files in [truck file format](technical/fileformat-truck).

Editorizer cannot create an empty truckfile, you need to copy a template and work from there.

```
New unnamed vehicle
; Vehicle name MUST be on the first line.
; Lines starting with ';' (semicolon) are comments

; ----- Required sections -----

globals
1000, 0.0, tracks/semi

nodes

beams

cameras

cinecam

; ----- Optional sections -----

; Engine makes the vehicle a land vehicle
engine
;min rpm, max rpm, torque, differential ratio, rear gear, first, second, third, fourth, fifth, sixth
1000.0, 2100.0, 6000.0, 4.10, 15.00,  18.00, 11.50, 6.00, 3.75, 2.75, 2.00, 1.50, 0.90, -1.0

wheels
0.4, 0.3, 12, 20, 20, 23, 1, 1, 3, 150.0, 400000.0, 3000.0, tracks/wheelface tracks/wheelband1
0.4, 0.3, 12, 23, 22, -25, 1, 1, 5, 150.0, 400000.0, 3000.0, tracks/wheelface tracks/wheelband1
0.4, 0.3, 12, 29, 28, 9999, 1, 1, 18, 150.0, 400000.0, 3000.0, tracks/wheelface tracks/wheelband1
0.4, 0.3, 12, 26, 27, 9999, 1, 1, 5, 150.0, 400000.0, 3000.0, tracks/wheelface tracks/wheelband1

; `forwardcommands` is for trucks, `importcommands` is for trailers
forwardcommands
importcommands

fileinfo

author chassis 69 yourname
author texture 69 yourname
author support 69 yourname

shocks

hydros

commands

rotators

ropes

ties

fixes

contacters

ropables

flares

props

exhausts

brakes

engoption

end
```

# Using blueprints

Blueprints are technical drawings of vehicles and machinery, very useful as reference. Many good blueprints can be found on the internet.

To load a blueprint, find _Blueprints_ in the top toolbar, and load in the files.

To adjust blueprints, click on _Place Blueprints_ on the far right, and place your blueprints in a desired position .

# Editing Nodes

When you want to add nodes, just click on _Add Nodes_ up in the right. Click where you want the node to go, either in the Top Left, Bottom Left or Botton Right areas. If you want to make the node only get placed on the "grid" that divides the areas up-check the "snap nodes to grid" box.
Special Nodes

Check [truckfile reference](technical/fileformat-truck) for special node types.

If you want to give your nodes these special options, just click on the _Nodes_ tab, pick the one you want to change, and put the corresponding node option in the options part.

# Editing Beams

When you want to add beams, just click on the _Add Beams_ up in the right. Click the first node where you want the beam to start. Click the second node which is where you want the beam to end.

Check [truckfile reference](technical/fileformat-truck) for special beam types.

If you want to give your beams these special options, just click on the _Beams_ tab, pick the beam you want to change, and put the corresponding beam option in the options box, along with any variables for that type of beam.

# Wheels

To add wheels, look at this example. Just click on the Wheels tab and add in the correct information in the correct spaces.

FRONT WHEELS(Steering wheels):

    wheels
    ; EXAMPLE: 
    0.5,0.1,12,33,34,9999,1,1,32,350.0,300000,4000, tracks/wheelface tracks/wheelband1
    ; EXAMPLE2: 
    0.5,0.1,12,35,36,9999,1,1,31,350.0,300000,4000, tracks/wheelface tracks/wheelband1 

REAR WHEELS:

    wheels
    ;EXAMPLE: 
    0.5,0.1,12,12,13,14,1,1,10,350.0,300000,4000, tracks/wheelfaceb tracks/wheelband1
    ;EXAMPLE2: 
    0.5,0.1,12,14,15,-12,1,1,9,350.0,300000,4000, tracks/wheelfaceb tracks/wheelband1 

# Scaling

To scale your vehicle if you find it a little bit too big, just go to the Visible Nodes tab at the very top. Click on Scale..., then put in decimal numbers from 0.01 to 0.99 in the X,Y,Z lines to scale it down, put in decimal numbers from 1.0 and up(experiment) to scale it up.

# Tools to avoid

In the _Visible Nodes_ tab at the top, I would advise to not use the _Interconnect_ or _Variable Interconnect_ options with any vehicle as it can mess up the structure and other things. Basically these options will join every node to every other node in the object... 
