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

The `Debug` tab in the Configurator and the `Debug` menu in-game contains a bunch of options used for various things, this page will explain to you what they all do.

# Configurator

As of RoR version 0.4.7.0, the Debug tab in the Configurator looks like this:
![1](/images/rorconfig-debug.png)

## Ingame Console

Displays a "live view" of the `RoR.log` in the console (shown by pressing `~` or by clicking on `Windows` -> `Show Console`)

![2](/images/debug-ingameconsole.png)

## Developer mode

Used by developers to unlock WIP features. Was used during 0.4.5's development for the (then unfinished) Multiplayer menu. May be used again in the future.

## Beam break/deform debug

Logs when beams get broken/deformed to the `RoR.log`, useful for finding exactly where a beam is broken/deformed. It does not currently work with [nodes2](http://docs.rigsofrods.org/vehicle-creation/fileformat-truck/#nodes2).

Examples:
```
YYY Beam 2681 just deformed with extension force 6106.08 / 6.4e+12. It was between nodes 49 and 31.
XXX Beam 2166 just broke with force 260145 / 223477. It was between nodes 136 and 132.
```
You can combine this with the `Ingame Console` option to see what beams get deformed/broken in the console:
![3](/images/debug-brokenbeamsingameconsole.png)

# Obsolete/broken options

These options either do not work in 0.4.7.0 or have been made obsolete.

## Debug Truck Mass
Prints node masses to the `RoR.log` when a vehicle is spawned, however this feature seems to not work in 0.4.7.0.

## Advanced Logging
Enables fancy HTML logs for loaded terrains, objects, and trucks. As this feature hasn't worked in a long time, it was removed by [this GitHub commit](https://github.com/RigsOfRods/rigs-of-rods/commit/06fbd8960926ed29d343ce81abb9dc32fb70410c).
 


