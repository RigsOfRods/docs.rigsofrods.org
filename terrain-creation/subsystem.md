== 0.4 Terrain system == The terrain system described here was introduced in version 0.4 and provides many new features and improved performance.

The previous terrain system was based upon Ogre engine's TerrainManager component, which was obsoleted, and thus RoR couldn't support it anymore.

**New Terrain Features:**

-   alpha splatting supported by the engine itself, no need to provide your own shader
-   improved speed: better LOD system
-   Global Light maps: Mountains will shadow the terrain if the sun is low, etc.
-   caching of terrain Data: the Terrain is generated on the first start and then written to cache (disk). The second start is then much faster.
-   integrated normal mapping
-   integrated parallax mapping
-   composite blend replacement: if you go away far enough, the alpha splats will be replaced by some rendered texture to improve speed.
-   Paging support: ability to load multiple pages of the terrain. (all at once only right now)
-   Edit-able, edit-ablity not implemented yet though x|

**File Type overview:**

-   **.terrn2**: Entry point for the terrain.Every terrain has one .terrn2
-   **.otc**: Configures the Ogre terrain, replaces the old .cfg format.
-   **.os** - Caelum system (sky/weather) config
-   **.hdx** - Hydrax config (0.4.5 and up)
-   **.png/./jpg/.dds** - Terrain textures and heightmap

### Terrain 2 (.terrn2) file format

``` bash
# ============================================================================== 
# *.terrn2 file = Entry point for RoR 0.4 map
#
# File is organized into sections denoted by [SectionName] lines.
# Sections consist of "key = value" pairs.
# Comments start with hash '#' character.
# Boolean values can be 1, true, yes | 0, false, no
# 
# ==============================================================================

# (Required) General section, provides basic info.
[General]

    # (String) Name of the map, displayed in menu.
    Name = YourMap
    
    # (FileName) File with terrain geometry info.
    GeometryConfig = YourMap.otc
    
    # (Boolean) Use water in the terrain?
    Water = 1
    
    # (Real) Height of water surface.
    WaterLine = -100
    
    # (Real) Height of the black ground plane
    WaterBottomLine = -120
    
    # (RGB, float notation) Color of the ambient light.
    AmbientColor = 1,1,1
    
    # (FileName) Config file for the Caelum system (sky/weather/sun).
    CaelumConfigFile = YourMap.os
    
    # (FileName) Config file for the Hydrax (water rendering)
    HydraxConfigFile = YourMap.hdx

    # (XYZ position) Starting position of player.
    StartPosition = 256, 10, 256
    
    # (String) Name of the cubemap (sky) to use.
    # You can use "tracks/skyboxcol" which comes with RoR.
    SandStormCubeMap = tracks/skyboxcol
    
    # (Real) Gravity power. Earth gravity is "-9.81". 
    Gravity = -9.81
    
    # (Integer) Category ID. Valid numbers for v0.4.0.7:
    #   129 = Addon Terrains
    #   5000 = Official Terrains
    CategoryID = 129

    # (Integer) Terrain version
    Version = 1
    
    # (GUID string) Required. Use generator link below.
    GUID = YourID
 
    # (Filename) Link to 'landuse' file. 
    TractionMap = YourMap-landuse.cfg

# (Optional) Authors, shown in menu.
[Authors]    

    # ("String = String" pairs) Contributed work = Name
    terrain = Yourname
    trees&grass = Yourname
    textures = Yourname
    objects = Yourname

# (Optional) Items placed on terrain.
[Objects]

    # Names of TerrainObject files, ending with "=".
    YourMapobj.tobj=
    YourMapMoreobj.tobj=
    
# Executable scripts asociated with the map.    
[Scripts]

    # Names of AngelScript files, ending with "=".
    SomeScripts.as=
    MoreScripts.as=
```

Generate GUID for your map: <http://www.guidgenerator.com/>

### Ogre Terrain Config (.otc)

``` bash
# ==============================================================================
# Ogre Terrain Config (.otc) file
# Defines heightmap, texture layers and shader options
#
# Format is INI without sections, `Key=Value` pairs, NO SPACES AROUND `=`!
# Boolean values can be: 1, true, yes | 0, false, no
# ==============================================================================
 
# (Integer, default 0) The number of terrain pages in X direction
# 0 means that you only have one page
PagesX=0
 
# (Integer, default 0) The number of terrain pages in Z (logical Y) direction
# 0 means that you only have one page
PagesZ=0
 
# (Integer, default 1025) How large is a page of tiles (in vertices)? Must be (2^n)+1
PageSize=1025
 
# The pagefile format
# Default: {MAP_NAME}-page-{X}-{Z}.otc
PageFileFormat=YourMap-{X}-{Z}.otc
 
# Heightmap.X.Y
# The heightmap options, specified per-page
Heightmap.0.0.raw.size=1025
Heightmap.0.0.raw.bpp=2
Heightmap.0.0.flipX=1
Heightmap.0.0.flipY=1
 
# (Boolean) Flat terrain? If true, no heightmap will be loaded.
Flat=false
 
# (Integer, default 1024) The world size of the terrain, in meters
# This setting is independent on heightmap resolution; for example using large heightmap with small world will yield in high-detail geometry.
WorldSizeX=1024
WorldSizeZ=1024
 
# (Integer, default 50) The factor with what the heightmap values get multiplied with
WorldSizeY=100
 
# (Integer, default 1024) Sets the default size of blend maps for a new terrain. This is the resolution of each blending layer for a new terrain.
LayerBlendMapSize=1024
 
# disableCaching=1 will always enforce regeneration of the terrain, useful if you want to change the terrain config (.otc) and test it. Does not cache the objects on it.
disableCaching=1
 
# =============
# optimizations
# =============
 
# (Integer, default 33) Minimum batch size (along one edge) in vertices; must be 2^n+1. 
# The terrain will be divided into tiles, and this is the minimum size of one tile in vertices (at any LOD).
minBatchSize=33
 
# (Integer, default 65) Maximum batch size (along one edge) in vertices; must be 2^n+1 and <= 65. 
# The terrain will be divided into hierarchical tiles, and this is the maximum size of one tile in vertices (at any LOD).
maxBatchSize=65
 
# (Boolean, default false) Whether to support a light map over the terrain in the shader, if it's present.
LightmapEnabled=false
 
# (Boolean, default false) Whether to support normal mapping per layer in the shader.
NormalMappingEnabled=false
 
# (Boolean, default false) Whether to support specular mapping per layer in the shader.
# IMPORTANT: Keep this enabled, otherwise  the specular map in the texture files won't be respected and your terrain will be ridiculously shiny.
SpecularMappingEnabled=true
 
# (Boolean, default false) Whether to support parallax mapping per layer in the shader.
ParallaxMappingEnabled=false
 
# (Boolean, default false) Whether to support a global colour map over the terrain in the shader, if it's present.
GlobalColourMapEnabled=false
 
# (Boolean, default false) Whether to use depth shadows.
ReceiveDynamicShadowsDepth=false
 
# (Integer, default 1024) Sets the default size of composite maps for a new terrain.
CompositeMapSize=1024
 
# (Integer, default 4000) Set the distance at which to start using a composite map if present.
CompositeMapDistance=4000
 
# (Integer, default 30) the default size of 'skirts' used to hide terrain cracks.
SkirtSize=30
 
# (Integer, default 1024) Sets the default size of lightmaps for a new terrain.
LightMapSize=1024
 
# (Boolean, default false) Whether the terrain will be able to cast shadows.
CastsDynamicShadows=false
 
# (Integer, default 5) Set the maximum screen pixel error that should  be allowed when rendering
MaxPixelError=3
 
# (Boolean, default false) dump the blend maps to files named blendmap_layer_X.png
DebugBlendMaps=false
```

### Ogre Terrain Page Config (.otc)

The terrain consists of pages. Number of pages is defined by PagesX and PagesZ (described above). There must be at least 1 page.

For each page, there must be an .otc file. File name format is set by PageFileFormat (described above). If there's just one page, it'll be named like "MapName-page-0-0.otc"

The page-config file specifies a heightmap to use for the page and terrain texture layers.

#### Format overview

-   **Line1:** Heightmap <span style="color:#BD0058">(file name)</span>. For example: my\_heightmap.png
-   **Line2:** Number of layers <span style="color:#BD0058">(integral number in range 1-6)</span> The OgreTerrain component has a limit of 6 layers (5 blendmaps)
-   **Line3 and further:** Layer definitions (see below)

#### Layer definitions

-   Lines starting with semicolon ''' ' ; ' ''' are comments
-   Layer definition line has these values, separated by ''' ' , ' ''' comma :
    -   **size** <span style="color:#BD0058">(real number 1-2048)</span> The target size of the texture on the terrain
    -   **diffusespecular** <span style="color:#BD0058">(file name)</span> The filename of the texture with the following format: RGB=Diffuse Color, A=Specular map
    -   **normalheight** <span style="color:#BD0058">(file name)</span> The filename of the texture with the following format: RGB=Normal map, A=Heightmap for parallax mapping
    -   **blendmap** <span style="color:#BD0058">(file name)</span> Blendmap texture file name
    -   **blendmapmode** <span style="color:#BD0058">(One capital letter: R / G / B / A)</span> Which color channel of the blendmap use for blending this layer.
    -   **opacity** <span style="color:#BD0058">(Real number 0-1)</span> Setting to 0 makes layer invisible.

Layer at position \#0 is a ground layer - it covers the entire page and thus needs no **blendmap**. It only accepts first 3 arguments: \[size\] \[diffusespecular\] \[normalheight\]

Layers \#1 - \#5 only cover areas which have a corresponding color in the **blendmap**.

#### Example

``` ini
31-heightmap.png
6
; Params: [worldSize], [diffusespecular], [normalheight], [blendmap], [blendmapmode], [alpha]
; The ground layer:
3.3  , 31-gravel_diffusespecular.dds , 31-gravel_normalheight.dds
; Other layers:
6    , 31-rock_diffusespecular.dds   , 31-rock_normalheight.dds   , 31-surfaces2.png, B, 0.9
5    , 31-sand_diffusespecular.dds   , 31-sand_normalheight.dds   , 31-surfaces2.png, G, 0.9
4    , 31-grass_diffusespecular.dds  , 31-grass_normalheight.dds  , 31-surfaces1.png, G, 0.8
3    , 31-asphalt_diffusespecular.dds, 31-asphalt_normalheight.dds, 31-surfaces1.png, R, 0.95
1024 , 31-shadow_diffusespecular.dds , 31-shadow_normalheight.dds , 31-shadow.png   , R, 0.8
```

### Terrain Objects (.tobj)

Defines object placement on terrain. More info: [Placing objects on terrains (For 0.38 and 0.4)](Placing_objects_on_terrains_(For_0.38_and_0.4) "wikilink")

Usage is equal to "terrn" files for 0.38 map system: [Terrn file description](Terrn_file_description "wikilink")

### Example Simple Terrain

Some examples of how the 0.4 terrain system is used:

-   [Simple2.zip](:Media:Simple2.zip "wikilink")

(add your own)

Old Terrain System (pre 0.4)
----------------------------

The old terrain system was very limited in sense of features and is obsolete since RoR version 0.4.0.

### Overview

**File Type overview:**

-   **.terrn** - You define terrain name, associated .cfg name, spawn point position, ambient colour and various object positions.
-   **.cfg** - You define Terrain Texture, RAW Heightmap file, World Sizes and Height, Tiles the map get divided into, Terrain LOD and additional stuff.
-   **.RAW** - A greyscale image which is the heightmap of the terrain.
-   **.os** - Caelum Config
-   **.png/./jpg/.dds** - Terrain Texture.

### How to upgrade an old Terrain to a 0.4 version terrain

Currently, the only way to convert to the 0.4 terrain system is by hand as the layer textures needs to be remapped due to the added features.

Just try to follow these steps (example with smallisland below):

-   preparational work:
    -   create a folder in Rigs of Rods 0.4\\terrains\\ (i.e. smallisland)
    -   unpack the files from the old terrain zip there

<!-- -->

-   create an empty text file named <>.terrn2 (smallisland.terrn2) with the following template:

``` ini
[General]
Name = 
GeometryConfig = 
Water=0
AmbientColor = 1, 1, 1
StartPosition =
CategoryID = 129
Version = 2
GUID = 

[Authors]
terrain = 

[Objects]
```

-   now fill that with info:
    -   Name : the terrain name that should be shown in the loader/chooser
    -   GeometryConfig : the terrain name + .otc (i.e. smallisland.otc)
    -   water: if "w" is provided in the old terrain file, add:
        -   Water=1
        -   WaterLine=72 (the 'w' value)
        -   WaterBottomLine=42 ( the 'w' value -30)
    -   StartPosition : the start position (X Y Z) without commas! take the first three values from the 5th or so line from the old config (REMOVE the commas!) (i.e. first three of: "147.346, 87.3784, 545.694, 147.346, 87.3784, 545.694, 147.346, 87.3784, 545.694")
    -   GUID: go to <http://www.guidgenerator.com/> and generate one
    -   Authors, terrain: name the old author

it should look like this atm:

``` ini
[General]
Name = Small Island
GeometryConfig = smallisland.otc
Water=1
WaterLine=72
WaterBottomLine=42
AmbientColor = 1, 1, 1
StartPosition = 147.346 87.3784 545.694
CategoryID = 129
Version = 2
GUID = bfd9e795-9f90-4b46-9a3b-4b48408d58ad

[Authors]
terrain = Pittras
update = tdev

[Objects]
```

next: create a text file named "smallisland.otc" (the name you provided under "GeometryConfig") with the following template:

``` ini
WorldSizeX=
WorldSizeZ=
WorldSizeY=

PageSize=
PageFileFormat=

Heightmap.0.0.raw.size=
Heightmap.0.0.raw.bpp=
Heightmap.0.0.flipX=

disableCaching=1
LightmapEnabled=0
NormalMappingEnabled=0
SpecularMappingEnabled=1
ParallaxMappingEnabled=0
GlobalColourMapEnabled=0
ReceiveDynamicShadowsDepth=0
```

now fill that out again:

-   WorldSizeX : Size of the world in X direction, find that value in the old .cfg file as "PageWorldX"
-   WorldSizeZ : Size of the world in Z direction, find that value in the old .cfg file as "PageWorldZ"
-   WorldSizeY : Multiplier of the heightmap in Y direction, find that value in the old .cfg file as "MaxHeight"
-   PageSize : Size of the heightmap, must be 2^n+1, take "PageSize" from the old .cfg, i.e. 1025
-   PageFileFormat: Specifies the formatting of the page filename. Format: "yourmap-page-0-0.otc"
-   If your terrain heightmap is in raw format provide the following settings:
    -   set Heightmap.0.0.raw.size to the value of "Heightmap.raw.size", i.e. Heightmap.raw.size=1025
    -   set Heightmap.0.0.raw.bpp to the value of "Heightmap.raw.bpp", i.e. Heightmap.raw.bpp=2
    -   If the Heightmap is filled in the old terrain ("Heightmap.flip=true"), then add "Heightmap.0.0.flipX=1" to the .otc

our example looks like this now:

``` ini
WorldSizeX=1000
WorldSizeZ=1000
WorldSizeY=300

PageSize=1025
PageFileFormat=smallisland-page-0-0.otc

Heightmap.0.0.raw.size=1025
Heightmap.0.0.raw.bpp=2
Heightmap.0.0.flipX=1

disableCaching=1
LightmapEnabled=0
NormalMappingEnabled=0
SpecularMappingEnabled=1
ParallaxMappingEnabled=0
GlobalColourMapEnabled=0
ReceiveDynamicShadowsDepth=0
```

next: create a text file named "smallisland-page-0-0.otc" (you already provided the filename format in the main smallisland.otc") with the following template:

``` ini
<heightmap filename>
< number of layers>
; worldSize, diffusespecular, normalheight, blendmap, blendmapmode, alpha
< size, diffusespecular, normalheight>
```

To avoid a shiny terrain, follow [this tutorial](http://www.rigsofrods.com/threads/109873-0-37-Content-Pack-Maps-0-4-0-7?p=1269382&viewfull=1#post1269382). The shininess is controlled by the alpha channel of your diffuse texture. A white (or missing) alpha channel means shiny, a black one matte.

Please notice that your alpha channel needs to be a bit brighter than completely black (RGB value of \[1, 1, 1\] instead of \[0, 0, 0\]), otherwise the alpha channel will not be saved.

Our example looks like this now:

``` ini
smallisland.raw
1
; worldSize, diffusespecular, normalheight, blendmap, blendmapmode, alpha
1000  , smallisland.dds, smallisland.dds
```

-   Upgrading the objects:
    -   create an entry under the "\[Objects\]" section in the terrn2-file for a filename followed by eqal, i.e.:

``` ini
[Objects]
smallisland.tobj=
```

Then create a text file named like that (i.e. "smallisland.tobj") and copy and paste all remaining lines from the old .terrn into that file. Leave out the "end". It is also possible to split the objects into multiple files.

-   You are done with the basics :)
-   You can download the example upgrade there: [Smallisland.zip](:Media:Smallisland.zip "wikilink")

The example looks like this at this point:

![](Smallisland.jpg "Smallisland.jpg")

Troubleshooting
---------------

-   Q: Why is everything so shiny?
    -   A: You might need to enable Specular Mapping (SpecularMappingEnabled=1) and darken the Alpha channel of your diffuse texture (it needs to be very dark to remove the shininess). [Click here for a tutorial](http://www.rigsofrods.com/threads/109873-0-37-Content-Pack-Maps-0-4-0-7?p=1269382&viewfull=1#post1269382).
-   Q: Why are procedural roads not working anymore?
    -   A: They are removed to be replaced by a better system in the near future.
-   Q: How to convert .RAW images?
    -   A: look there: [Creating\_a\_raw\_file\#Automated\_Image\_to\_raw\_file\_Bat\_scripts](Creating_a_raw_file#Automated_Image_to_raw_file_Bat_scripts "wikilink")
-   Q: how to create the strange texture format the terrain uses with the different channels?
    -   A: look there as well: <http://www.ogre3d.org/tikiwiki/tiki-index.php?page=Ogre+Terrain+Textures>

