---
title: "Debugging options"
layout: page
categories: [gameplay]
---

<div class="toc" markdown="1">
  * TOC
  {:toc}
</div>

# Introduction

The `Debug` tab in the Configurator and the `Debug` menu in-game contains a bunch of options used for debugging various RoR features, this page will explain to you what they all do.

# Configurator

As of RoR version 0.4.7.0, the Debug tab in the Configurator looks like this:
![1](/images/rorconfig-debug.png)

## Ingame Console

Displays a "live view" of the `RoR.log` in the console (shown by pressing `~` or by clicking on `Windows` -> `Show Console`)

![2](/images/debug-ingameconsole.png)

## Developer mode

Used by developers to unlock WIP features. Was used during 0.4.5's development for the (then unfinished) Multiplayer menu. May be used again in the future.

## Debug Truck Mass
Prints node masses to the `RoR.log` when a vehicle is spawned, This feature does not work in the current official version (0.4.7.0), but has been fixed in upcoming version 0.4.8.0.

Example:
```
Node 0 : 405 kg (normal load node: 2800 kg / 8 nodes)
Node 1 : 405 kg (normal load node: 2800 kg / 8 nodes)
Node 2 : 405 kg (normal load node: 2800 kg / 8 nodes)
Node 3 : 405 kg (normal load node: 2800 kg / 8 nodes)
Node 4 : 412 kg (normal load node: 2800 kg / 8 nodes)
Node 5 : 412 kg (normal load node: 2800 kg / 8 nodes)
Node 6 : 412 kg (normal load node: 2800 kg / 8 nodes)
Node 7 : 412 kg (normal load node: 2800 kg / 8 nodes)
Node 8 : 50 kg
TOTAL VEHICLE MASS: 3323 kg
```

## Advanced Logging
Enables fancy HTML logs for loaded terrains, objects, and trucks. As this feature hasn't worked in a long time, it was removed by [this GitHub commit](https://github.com/RigsOfRods/rigs-of-rods/commit/06fbd8960926ed29d343ce81abb9dc32fb70410c).


## Beam break/deform debug

Logs when beams get broken/deformed to the `RoR.log`, useful for finding exactly where a beam is broken/deformed. It does not currently work with [nodes2](http://docs.rigsofrods.org/vehicle-creation/fileformat-truck/#nodes2).

Examples:
```
YYY Beam 2681 just deformed with extension force 6106.08 / 6.4e+12. It was between nodes 49 and 31.
XXX Beam 2166 just broke with force 260145 / 223477. It was between nodes 136 and 132.
```
You can combine this with the `Ingame Console` option to see what beams get deformed/broken in the console:
![3](/images/debug-brokenbeamsingameconsole.png)

## Debug VideoCameras

Displays lines to help position videocameras. This feature does not work in the current official version (0.4.7.0), but has been fixed in upcoming version 0.4.8.0:

![3](/images/debug-videocameras.png)

## Debug EnvironmentMapping / Chrome

Displays an unwrapped cube on what is used to display the reflections on vehicles. This feature does not seem to work on 0.4.7.0 or the latest upstream.


## Trigger Debug

Logs messages to the `RoR.log` relating to [triggers](http://docs.rigsofrods.org/vehicle-creation/fileformat-truck/#triggers).

Example:
```
Trigger Longbound activated. Trigger BeamID 1457 Triggered F4
Trigger Longbound activated. Trigger BeamID 1458 Triggered F4
Trigger Longbound activated. Trigger BeamID 1461 Triggered F8
Trigger Longbound activated. Trigger BeamID 1462 Triggered F4
```

## Debug Collision Meshes

Displays the collision meshes on objects, used for debugging collision mesh issues or for displaying event boxes (e.g. creating a custom truckshop or a scripted event):

![4](/images/scripting-odef-eventbox-debug-1.jpg)

## Depth of Field Debug

Displays a box on the top right corner of the screen to help with debugging DOF problems:

![5](/images/debug-dof.png)

## Input Grabbing

Determines the input capture mode, default is `All`. `Dynamically` should be used if you're running RoR in windowed mode.

## Preselected Map/Truck

Skips the selector windows and loads a specified terrain/vehicle on startup.

Example:

![6](/images/debug-preselectedmaptruck.png)



