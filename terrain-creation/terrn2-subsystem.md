---
layout: page
title:  "Terrain subsystem (Terrn2)"
categories: [terrain-creation]
---

<div class="toc" markdown="1">
* TOC
{:toc}
</div>

This is a technical reference of terrain system in Rigs of Rods. It provides commented examples of various files needed to compose a terrn2 terrain.

If you're new to terrain creation, read [intro to terrain creation](/terrain-creation/intro) first.

<br> <!-- Ugly hack to make space for TOC -->
<br>
<br>
<br>

# Terrain 2 (.terrn2) file format

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
    WaterLine = 6
    
    # (Real) Height of the black ground plane
    WaterBottomLine = -150
    
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

# Ogre Terrain Config (.otc)

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
# This setting is independent on heightmap resolution;
# for example using large heightmap with small world will yield in high-detail geometry.
WorldSizeX=1024
WorldSizeZ=1024
 
# (Integer, default 50) The factor with what the heightmap values get multiplied with
WorldSizeY=100
 
# (Integer, default 1024) Sets the default size of blend maps for a new terrain.
# This is the resolution of each blending layer for a new terrain.
LayerBlendMapSize=1024
 
# disableCaching=1 will always enforce regeneration of the terrain,
# useful if you want to change the terrain config (.otc) and test it.
# Does not cache the objects on it.
disableCaching=1
 
# =============
# optimizations
# =============
 
# (Integer, default 33)
# Minimum batch size (along one edge) in vertices; must be 2^n+1. 
# The terrain will be divided into tiles,
# and this is the minimum size of one tile in vertices (at any LOD).
minBatchSize=33
 
# (Integer, default 65)
# Maximum batch size (along one edge) in vertices; must be 2^n+1 and <= 65. 
# The terrain will be divided into hierarchical tiles,
# and this is the maximum size of one tile in vertices (at any LOD).
maxBatchSize=65
 
# (Boolean, default false)
# Whether to support a light map over the terrain in the shader, if it's present.
LightmapEnabled=false
 
# (Boolean, default false) Whether to support normal mapping per layer in the shader.
NormalMappingEnabled=false
 
# (Boolean, default false) Whether to support specular mapping per layer in the shader.
# IMPORTANT: Keep this enabled, otherwise  the specular map in the texture files
# won't be respected and your terrain will be ridiculously shiny.
SpecularMappingEnabled=true
 
# (Boolean, default false) Whether to support parallax mapping per layer in the shader.
ParallaxMappingEnabled=false
 
# (Boolean, default false)
# Whether to support a global colour map over the terrain in the shader, if it's present.
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
 
# (Integer, default 5)
# Set the maximum screen pixel error that should  be allowed when rendering
MaxPixelError=3
 
# (Boolean, default false) dump the blend maps to files named blendmap_layer_X.png
DebugBlendMaps=false
```

# Ogre Terrain Page Config (.otc)

The terrain consists of pages. Number of pages is defined by PagesX and PagesZ (described above). There must be at least 1 page.

For each page, there must be an .otc file. File name format is set by PageFileFormat (described above). If there's just one page, it'll be named like "MapName-page-0-0.otc"

The page-config file specifies a heightmap to use for the page and terrain texture layers.

## Format overview

-   **Line1:** Heightmap <span style="color:#BD0058">(file name)</span>. For example: my\_heightmap.png
-   **Line2:** Number of layers <span style="color:#BD0058">(integral number in range 1-6)</span> The OgreTerrain component has a limit of 6 layers (5 blendmaps)
-   **Line3 and further:** Layer definitions (see below)

## Layer definitions

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

For explanation of used images, see [Images & color channels](/tools-tutorials/images-color-channels)

## Example

``` bash
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

# Terrain Objects (.tobj)

Defines object placement on terrain. More info: [Static objects](/terrain-creation/intro/#static-objects-1)


