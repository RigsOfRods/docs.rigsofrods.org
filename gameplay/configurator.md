---
layout: page
title:  "Configurator"
categories: [gameplay]
---

<div class="toc" markdown="1">
  * TOC
  {:toc}
</div>

![](/images/rorconfig.png)

This is the configurator. It is how you set the options for how RoR looks and how it plays. It is also how you access multiplayer servers.

# Video tutorial

<iframe width="640" height="480" src="https://www.youtube.com/embed/z60VoTbJao0" frameborder="0" allowfullscreen></iframe>

# Settings

## Render System

-   **Render System** - The rendering system to use. Either D3D9 or OpenGL on Windows, or just OpenGL on Linux/Mac.
-   **FSAA** - The amount of full screen antialiasing you want.
-   **Full Screen** - The window type you want, either Full Screen or Windowed.
-   **Rendering Device** (Windows)/**RTT Mode** (Linux)/**???** (Mac)
-   **VSync** - Turns on [vertical synchronization](http://en.wikipedia.org/wiki/Vertical_sync).
-   **Video Mode** - The resolution you want to play RoR at. Custom resolutions can be specified in [ogre.cfg](ogre.cfg "wikilink"), but note that the truck HUD will not scale properly.

## Graphics

-   **Texture Filtering** - The type of filtering to do on textures.
-   **Sky Type** - Type of horizon/sky to use. Sandstorm is essentially no sky while Caelum has a sky and sun with clouds and artificial time.
-   **Shadow Type** - The shadow technique to use.
-   **Sightrange** - How far to draw objects.
-   **Shadow Performance Optimization** - Disables vehicle shadows when in first person view.
-   **Water type** - What water rendering technique to use.
-   **Enable Waves** - Exactly what it says.
-   **Vegetation** - The level of vegetation on supported maps.
-   **Enable Particle Systems** - Show particles, like dust, smoke and water splashes.
-   **Mirrors** - Enable mirrors inside vehicle cockpits/cabins.
-   **HDR** - Enable High Dynamic Range Lighting.
-   **High quality reflective effects** - Enable reflections on vehicles that support it.
-   **DOF** - Enable depth of field effect.
-   **Screenshot Format** - What format to save screenshots in.

## Gameplay

-   **Language** - Language to use.
-   **Default Gearbox Mode** - Default mode for gearbox on cars.
-   **FOV External** - Field of View for external cameras.
-   **FOV Internal** - Field of View for internal cameras.
-   **Disable Camera Pitching** - Disables external camera pitching.
-   **User Token** - User token for Multiplayer.
-   **disable creak sound** - Disables creaking sound.

## Advanced

-   **Sound Device** - What device to drive for sounds.
-   **Thread number** - How many threads RoR can use.
-   **Light Source effects** - What lights can illuminate objects.
-   **Regen Cache** - Regenerates Cache.
-   **Clear Cache** - Clears Cache.
-   **Replay Mode** - Enable replay mode.
-   **Enable Position Storage** - Enable position storage.
-   **Hydrax Water System** - Experimental high quality water effects. Windows only!
-   **Disable Overview Map** - For experimenting only!

## Debug

-   **Ingame Console** - Enables scripting console ingame.
-   **Debug Truck Mass** - Output mass of every node of a truck in [RoR.log](/gameplay/jargon#rorlog)
-   **Advanced Logging** - Fancy HTML logs for objects, terrains and trucks.
-   **Beam Break Debug** - Logs beam info to log when beam breaks.
-   **Beam Deform Debug** - Logs beam info to log when beam deforms.
-   **Debug VideoCameras** - Adds virtual camera mesh to help position the camera correctly.
-   **Debug EnvironmentMapping / Chrome** - Displays unwraped cube of what is used for reflections on vehicles.
-   **Trigger Debug** - Enables Trigger debug messages.
-   **Debug Collision Meshes** - Shows collision meshes to help position them correctly.
-   **Enable Depth of Field Debug** - Shows DOF debug display.
-   **Disable Crash reporting** - Disables crash handling system.
-   **Input Grabbing** - How the mouse will be detected.
-   **Preselected Map** - Map selected at startup.
-   **Preselected Truck** - Truck selected at startup.

# Controls

See [controls and configuration](/gameplay/controls-config)

# About

Shows detailed information about the version, build date, ect. Also shows credits and used libraries.
