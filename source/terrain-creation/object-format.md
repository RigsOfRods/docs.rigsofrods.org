Object format (.odef)
============



## Introduction

The `.odef` format specifies a static object that can be placed on a terrain. 
These files are placed in the same zip as the object's mesh files. Rigs of Rods will not load the object if the file does not exist!     


Basic example with a collision mesh:   
<br>
```
Building.mesh
1, 1, 1

beginmesh
mesh BuildingCollision.mesh
endmesh

end
```

Advanced example file featuring event boxes:

```
hangar.mesh
1, 1, 1

beginmesh
mesh hangarcol.mesh
endmesh


beginbox
boxcoords -23.75, -21.75, -0.2, 2.1, -3.07, -0.19
virtual
event shopplane avatar
reverb_preset EFX_REVERB_PRESET_WOODEN_ALCOVE
endbox

beginbox
boxcoords  -17, 17, 0, 4.5, -29, 4
virtual
event spawnzone
reverb_preset EFX_REVERB_PRESET_FACTORY_HALL
direction 0, 90, 0
endbox

end
``` 

The format is described below: 

The first line specifies the visual mesh to use. Can be set to `none` to disable visuals, useful for event boxes. 

The second line specifies the scale of it (`x`, `y`, `z`) 
Default: `1,1,1`

After that, several sections can follow (`beginbox`, `beginmesh`, `playanimation`) 

The `.odef` file must be always closed with `end`

If there are no Begin box nor Begin mesh sections, the object will have no collisions. 

## Commands 

These commands can be called outside or inside a `beginbox` or `beginmesh`:

### setMeshMaterial

`setMeshMaterial tracks/bigsign/town` 

 You can create different materials (red, blue, green skins) for your object and now, you only need to create 3 different `.odef` files, one for each color. 

For example you create a file called `myRedBuilding.odef` and inside you specify `setMeshMaterial myRedColor`, `myRedColor` is defined on any `.material` file you need to create.

### nocast

Disables shadow casting for the object, useful for skyboxes.

```
Building.mesh
1, 1, 1

beginmesh
mesh BuildingCollision.mesh
endmesh

nocast

end
```



## Begin box 

Specifies a box that can be used for collisions or events.

`boxcoords x, x1, y, y1, z, z1` where the upper near left vertex of the 3D box is (`x`, `y`, `z`) and the lower far right vertex of the box is (`x1`, `y1`, `z1`). If you are defining a collision box, you don't need any other optional commands, just `endbox`. 

**optional:** `virtual`: this makes the box to spawn an event. In this case you must also have an event line in this box: 

**optional:** `event eventname filterevent` 

`eventname`: the name of the event it should generate. 

Some predefined values are `shopboat`, `shoptruck`, `shopplane`, `shoptrain` and `spawnzone` but you can define a non existing eventname if you want to use with Angelscript.

`filterevent`: on what it should trigger. valid values: `avatar`, `truck`, `truck_wheels`, `boat` and `airplane`. 

**optional:**`direction 0, 90, 0`: this determines the direction of objects spawned in this box 

**optional:**`camera x, y, z`: Coordinates to place the camera. 

**optional:**`forcecamera x, y, z`: Coordinates to place the camera, and force to change to this camera point of view when player enter at the box coords. 

**optional:**`reverb_preset preset_name`:  The OpenAL sound preset to be used when player vehicle enters the box. 
Where `preset_name` is an `EFX_REVERB_PRESET_*` from [here](https://github.com/RigsOfRods/rigs-of-rods/blob/4261db5063f47921f0305fb491a12eda6c297aa4/source/main/audio/SoundManager.cpp#L327-L401).

`endbox` must close the box

```
beginbox
boxcoords -23.75, -21.75, -0.2, 2.1, -3.07, -0.19
virtual
event shopplane avatar
endbox
``` 

Whenever the character (RoRbot) enters the box specifies by boxcoords, a trigger `shopplane` will be triggered, so the spawn menu will be shown.

## Begin mesh

You can use a existing mesh that RoR collision system will use. 

`beginmesh`: this enables you to use meshes for collisions: 

`mesh hangar.mesh`: this load the mesh hangar.mesh as a collision mesh. Important: Only use very low polygon meshes, or the simulation will be slowed down drastically! 

`endmesh`: closes the actual mesh box

## Friction

Defined inside of a `beginbox` or `beginmesh`, this sets the friction of a collision mesh or box. If not defined the default groundmodel used will be `concrete`.

`frictionconfig name-groundmodel.cfg` 

Optional, loads a custom groundmodel config. Use this if you want to use a groundmodel not specified in [ground_models.cfg](https://github.com/RigsOfRods/rigs-of-rods/blob/master/resources/skeleton/config/ground_models.cfg).

`name-groundmodel.cfg` is the name of your groundmodel config file. 

`stdfriction name`  or `usefriction name`

Where `name` is either `concrete`, `asphalt`,`gravel`, `rock`, `ice`, `snow`, `metal`, `grass` or `sand`: this will set the type of friction the collision mesh or box will do. The physical parameters of these standard friction materials are defined in the configuration file [ground_models.cfg](https://github.com/RigsOfRods/rigs-of-rods/blob/master/resources/skeleton/config/ground_models.cfg).

For example, if you have made a road object and you want to give it an asphalt friction, give it an odef file like this one:

```
example_road.mesh
1, 1, 1

beginmesh
mesh example_road.mesh
stdfriction asphalt
endmesh

end
```

A friction settings tool can be accessed in-game through the Tools tab of the Top Menubar. Use this to check if the friction is correctly applied to the object.

## Animations

If your object has an animation you can play it with this additional line: 

`playanimation speedfactorMin speedfactorMax AnimationName`

Example from the terrain [Fall Run](http://forum.rigsofrods.org/resources/fall-run.149/):

`playanimation 0.5, 0.6, CAT_330c_diging`

Notes: These objects wont be collide-able, and the animation will loop forever 

## Particles

You can add chimneys or other particle effects to your object using this:

```
;particleSystem scale, x, y, z, particleInstanceName particleScriptName
particleSystem 1, 1, 1, 1, myfire1 enhancedFire
```

## Ambient light

Allows for ambient light to be added to an object that can cast light onto other objects.  Works similarly to [flares](../vehicle-creation/fileformat-truck.md#flares).

!!! note
	Light casting currently only works with PSSM shadows disabled!

### Pointlight

```
;pointlight x, y, z, dirx, diry, dirz, r, g, b, range
pointlight -13, 1, 6, -1, 0, -1, 10, 5, 0, 60
```

Parameters:

- X position: Light's X coordinate.
- Y position: Light's Y coordinate.
- Z position: Light's Z coordinate.
- DirX: Light direction on the X axis.
- DirY: Light direction on the Y axis.
- DirZ: Light direction on the Z axis.
- R, G, B: RGB 0-1 color values. Sets the color of the visual flare and light.
- Range: Distance the light will cast.

### Spotlight

```
;spotlight x, y, z, dirx, diry, dirz, r, g, b, range, innerAngle, outerAngle 
spotlight  -13, 1, 6, -1, 0, -1, 10, 5, 0, 60,30,45
```

Parameters:

- X position: Light's X coordinate.
- Y position: Light's Y coordinate.
- Z position: Light's Z coordinate.
- DirX: Light direction on the X axis.
- DirY: Light direction on the Y axis.
- DirZ: Light direction on the Z axis.
- R, G, B: RGB 0-1 color values. Sets the color of the visual flare and light.
- Range: Distance the light will cast.
- Inner / Outer Angle: The angles that determine where the light fades from bright in the middle to dimmer on the outside edges.
