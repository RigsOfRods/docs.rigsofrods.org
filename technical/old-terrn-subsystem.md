---
layout: page
title:  "Old Terrain System (pre 0.4)"
categories: [technical]
---

This subsystem is obsolete since RoR version 0.4.0.
It was based upon Ogre engine's TerrainManager component,
which was obsoleted, and thus we couldn't rely on it anymore.

# File type overview

-   **.terrn** - You define terrain name, associated .cfg name, spawn point position, ambient colour and various object positions.
-   **.cfg** - You define Terrain Texture, RAW Heightmap file, World Sizes and Height, Tiles the map get divided into, Terrain LOD and additional stuff.
-   **.RAW** - A greyscale image which is the heightmap of the terrain. It is a RAW 8/16 bit DEM (digital elevation map). 
    Its dimensions MUST BE squared sized and with size (2^n) + 1, in example 1025x1025.
    As a consequence, the total file size must be 2,101,250 bytes (2x1025x1025).
    Other elevation sized maps could be: 129x129, 513x513, 2049x2049 
-   **.os** - Caelum Config
-   **.png/./jpg/.dds** - Terrain Texture, typically a large bitmap (for example a 1024x1024 BMP) that is projected onto the terrain.
    This texture must include shading and shadowing (the terrain is not shaded by RoR).
    The light source (the sun) heading is -60 degree and altitude of 25 degree.
-   **.png/./jpg/.dds** - A miniature map: a 256x256 image (that can be the reduction of the texture file) used as a map in RoR. 

# Converting Terrn format to Terrn2 format

Currently, the only way to convert to the 0.4 terrain system is by hand as the layer textures needs to be remapped due to the added features.

## Steps

* Unpack files from old terrain zip to a directory
* Create .terrn2 file [from template](terrn2-subsystem.html#terrain-2-terrn2-file-format).
    * Water: if "w" is provided in the old terrain file, set:

        Water           = 1                      ```<br>
        WaterLine       = 72 (the 'w' value)     ```<br>
        WaterBottomLine = 42 ( the 'w' value -30)```

    * Start position: the start position (X Y Z) without commas!
      take the first three values from the 5th or so line from the old config (REMOVE the commas!)
      (i.e. first three of: "147.346, 87.3784, 545.694, 147.346, 87.3784, 545.694, 147.346, 87.3784, 545.694")
* Create a file YourMapName.otc (the name you provided under "GeometryConfig") [from template](terrn2-subsystem.html#ogre-terrain-config-otc).
    -   WorldSizeX : Size of the world in X direction, find that value in the old .cfg file as "PageWorldX"
    -   WorldSizeZ : Size of the world in Z direction, find that value in the old .cfg file as "PageWorldZ"
    -   WorldSizeY : Multiplier of the heightmap in Y direction, find that value in the old .cfg file as "MaxHeight"
    -   PageSize : Size of the heightmap, must be 2^n+1, take "PageSize" from the old .cfg, i.e. 1025
    -   PageFileFormat: Specifies the formatting of the page filename. Format: "yourmap-page-0-0.otc"
    -   If your terrain heightmap is in raw format provide the following settings:
        -   set Heightmap.0.0.raw.size to the value of "Heightmap.raw.size", i.e. Heightmap.raw.size=1025
        -   set Heightmap.0.0.raw.bpp to the value of "Heightmap.raw.bpp", i.e. Heightmap.raw.bpp=2
        -   If the Heightmap is filled in the old terrain ("Heightmap.flip=true"), then add "Heightmap.0.0.flipX=1" to the .otc
* Create a file named "yourmap-page-0-0.otc" (specified in previous .otc) [from template](terrn2-subsystem.html#ogre-terrain-page-config-otc).
* Create a file yourmap.tobj (filename specified in .terrn2 under [Objects])
  and copy and paste all remaining lines from the old .terrn into that file.
  Leave out the "end". It is also possible to split the objects into multiple files.

## Tips

Avoid a shiny terrain. The shininess is controlled by the alpha channel of your diffuse texture.
A white (or missing) alpha channel means shiny, a black one matte. It needs to be very dark
to remove the shininess. You also need to enable Specular Mapping (```SpecularMappingEnabled=true```)

Please notice that (in some image editors) your alpha channel needs to be a bit brighter
than completely black (RGB value of \[1, 1, 1\] instead of \[0, 0, 0\]), otherwise
the alpha channel will not be saved.

Do not use procedural roads. They have been disabled.

How to create the strange texture format the terrain uses with the different channels?
Look there as well: <http://www.ogre3d.org/tikiwiki/tiki-index.php?page=Ogre+Terrain+Textures>

