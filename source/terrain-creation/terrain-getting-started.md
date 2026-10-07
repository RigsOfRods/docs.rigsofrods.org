Getting started creating terrains
=================================

Rigs of Rods doesn't have a fully-featured terrain editor tool - to build a terrain from the ground up,
you will have to use external tools and know what files in what formats to create and edit.
The game allows some terrain editing (placing and moving objects, creating roads...)
and more features are in the works.
This document will guide you through the features and mechanics offered by the game
while reffering you to in-depth pages for details or dedicated tutorials for tools.

Info for player
---------------

You'll want to give your terrain a name, some description, a maximum size and likely a preview image,
so that the players can pick a terrain to play. All these infos live in [a TERRN2 file](terrn2-subsystem/#terrain-2-terrn2)
where you also specify what features you want to use and what other files to load. The TERRN2 file formats
is central to the map creation process and will come up multiple times in this guide.

The landscape
-------------

Rigs of Rods uses **heightmaps** (a.k.a elevation maps) to specify the terrain shape, both visibly and physically.
Recognized file formats are gray-scale PNG images (Portable Network Graphics) which are always 8-bit
and RAW files which may be 8-bit or 16-bit. To create a heightmap, you can use a simple painting program for the PNG
or a dedicated terrain generator like [L3DT](l3dt-map-making). To load the heightmap in game,
you need to create [a couple OTC files](terrn2-subsystem/#ogre-terrain-config-otc) and reference them from
[your TERRN2 file](terrn2-subsystem/#terrain-2-terrn2).
 
The ground surface
------------------

The visual appearence and the physical traversability are defined separately,
although both use **color-coded images** (usually PNGs) for their distribution,
so you can reuse the same colormaps for both cases.

The visuals are done using classic **image textures** (DDS, PNG etc...) 
and basic shading techniques (normal mapping, specular mapping, parallax mapping) are provided out-of-the-box.
Texturing the terrain is done by [specifying layers in the OTC files](terrn2-subsystem/#layer-definitions).

The physical properties are specified as [ground models](https://github.com/RigsOfRods/rigs-of-rods/blob/master/resources/skeleton/config/ground_models.cfg).
Their placement on terrain is done with [a Traction Map (a.k.a. LandUse) file](terrn2-subsystem/#traction-map-cfg)
referenced from [the TERRN2 file](terrn2-subsystem/#terrain-2-terrn2) definition.

Water surface
-------------

Like many games, Rigs of Rods has a global water level specified in [the TERRN2 file](terrn2-subsystem/#terrain-2-terrn2).
Water is somewhat under-developed; the popular HydraX system has random waves which don't affects physics though,
other options have physical waves specified in [wavefield.cfg](https://github.com/RigsOfRods/rigs-of-rods/blob/master/resources/skeleton/config/wavefield.cfg)
but underwhelming visuals. Players can also use in-game console to change water level during gameplay.

Sky and weather
---------------

This aspect of terrain is quite incomplete and currently under development.
The simplest option for both player (via game settings) and modder (via [TERRN2](terrn2-subsystem/#terrain-2-terrn2))
is **a sky box** which has no weather or day/night cycle, only configurable ambient light color and intensity.

The most popular sky system at player's option is **Caelum**. It has day/night cycle (adjustable in-game by top menubar)
and map author can configure clouds and weather using [Caelum sky def](https://github.com/RigsOfRods/rigs-of-rods/blob/master/resources/caelum/RoRSkies.os)
file (the .OS suffix stands for 'Ogre Script') which must be referenced from (via [TERRN2](terrn2-subsystem/#terrain-2-terrn2)) file.
Work is currently being done to replace Caelum's texture-based clouds and billboard sun
with volumetric clouds and light scattering sun borrowed from the SkyX subsystem.

Vegetation
----------

Whether a lush or desert location, a vegetation system will come in handy, even if utilized for rocks and rubble instead of flora.
Vegetation is defined using keywords [`grass`](terrn2-subsystem/#grass)
and [`trees`](terrn2-subsystem/#trees) in the [Terrain Objects (.TOBJ)](terrn2-subsystem/#terrain-objects-tobj) file format.
Both use **color-coded images** (usually PNGs) for their distribution, so you can reuse the same colormaps from surface/traction definitions.
Grass is generated procedurally from provided image textures and parameters, trees repeat supplied mesh. Both support randomization and variances.

Structures
----------

Stand-alone static objects like houses, garages or hangars, even traffic lights and road signs are each defined using
[Object Definition (.ODEF)]() file and placed on terrain using the [Terrain Objects (.TOBJ)](terrn2-subsystem/#terrain-objects-tobj) 
file format (see also [editing objects tutorial](editing-terrain-objects)).
Objects can be added/moved/deleted in-game using a console (activated by '~' or from top menubar)
and editor mode (activated using 'Ctrl+Y' key combo or via top menubar). 
Use `help` console command and [moving objects](editing-terrain-objects/#moving-objects) guide for more information.

Dynamic structures like static cranes, draw bridges, rail junctions and so on are defined like vehicles or loads
using the [truck fileformat](vehicle-creation/fileformat-truck/) with some of it's nodes [fixed in place](vehicle-creation/fileformat-truck/#fixes).
They're also placed on terrain using the [Terrain Objects (.TOBJ)](terrn2-subsystem/#terrain-objects-tobj) and can be moved using the editor mode.

Roads and bridges
-----------------

The game provides a fully featured [road editor](terrn2-subsystem/#road-editor)!
Terrains are saved as splines in the [TOBJ files](terrn2-subsystem/#procedural-roads).
Bridges are made as elevated roads.

Railroads
---------

The game supports standard-gauge railroads and offers a selection of locomotives and railcars, as well as railroad structures like train depos, cranes and stations.
Unfortunately, railroads cannot yet be created freely like roads - development is uderway.
Rails are offered as pre-made ODEF pieces (including .FIXED switches) which you can build a network from, but you're limited to completely flat layout.
See [Building rail tracks](building-rail-tracks) guide.

Airports and seaports
---------------------

These are made entirely from pre-made ODEF pieces.
To view a list in game, go to top menu 'Tools', option 'Browse gadgets' and select 'ODEF browser'.

Race tracks
-----------

Races are defined using .RACETRACK files (each file specifies a single race track). 
In .terrn2, put the race files under section `[Races]` - Filenames must include extension and end with = (like scripts do).
```
racetrack_name Autocross
racetrack_laps 1
; static objects (.ODEF) to use on track:
racetrack_checkpoint_object 31-checkpoint
racetrack_start_object 31-checkpoint
racetrack_finish_object 31-checkpoint

; Race system supports branching/joining paths!
; Checkpoint format: checkpointNum(1+), altpathNum(1+), x, y, z, rotX, rotY, rotZ, objName(override, optional)
; By convention, the checkpoint meshes are oriented sideways (facing X axis)
begin_checkpoints
1, 1, 916, 9, 454, 0, 0, 0
2, 1, 914, 9, 390, 0, 15, 0
; ... snip ...
11, 1, 871, 9, 475, 0, 180, 0
12, 1, 897, 9, 524, 0, -120, 0
end_checkpoints
```

A legacy method of defining races is [using AngelScript](terrn2-subsystem/#scripts-section) together with [online race generator](race-generator/).
