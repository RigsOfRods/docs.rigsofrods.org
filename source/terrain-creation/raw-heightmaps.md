Heightmap RAW files
============

!!! warning "Outdated"
	This tutorial is from 2007, written for Blender version 2.43. It remains here as it contains some useful information. 


A "heightmap", or "elevation map", is an image or binary file where every pixel/number represents world height at the given point.
RoR supports 8-bit or 16-bit unsigned integer RAW heightmaps.


## Making heightmaps in Blender

Blender is open source, cross platform, and free. 
You can also use it to generate meshes, truck and load files, 
someone who uses blender to make trucks is already familiar with the interface and can easily start making terrains. 
Plus blender can go into great detail with the terrain surface and allow the user to move individual modes at will. 
Blender can also export a 16bit grayscale image, which is required by RoR.

### Requirements
[Blender](https://www.blender.org/) with EXR support (v2.43+ maybe earlier)<br/>
[ImageMagick](https://imagemagick.org/index.php) with EXR support (v6.3.4+)


### Setting up the Environment

<img src="/images/heightmaps-blender-01-eraseall.png">

* Start up <code>blender</code>, in Linux use the <code>-w</code> switch to have blender use a managed window.
* Press the (key|a) key to select all objects (all objects turn pink when selected)
* Press the (key|x) key and a little dialog pops up under the cursor, click <code>Erase Selected Object(s)</code> to erase all the objects.


### Add a Plane

<a href="/images/heightmaps-blender-02-addplane.png"><img src="/images/heightmaps-blender-02-addplane.png"></a>
<a href="/images/heightmaps-blender-03-plane2x2.png"><img src="/images/heightmaps-blender-03-plane2x2.png"></a>

* Press the (key|numpad 7) key to look at the xy plane.
* Press the (key|spacebar) and in the menu that appears select <code>''Add''</code>-><code>''Mesh''</code>-><code>''Plane''</code>


At this point you have a 2x2 BU (blender units) plane centered at 0,0,0 (see above image). 
What we want is a 3x3 BU plane centered at 1.5,1.5,0. this isn't needed but it sets up an easy conversion factor of 1BU = 1km. 
So when you look at the width on an edge a 0.001BU = 1 meter.

### Scaling and moving the Plane

<a href="/images/heightmaps-blender-04-scaleplane.png"><img src="/images/heightmaps-blender-04-scaleplane.png"></a>

* make sure you are in <code>Edit Mode</code>(<img src="/images/blender-old-editmode.png">).
* Press the (key|s) key to scale the plane, and hold down the the (key|ctrl) to snap to the grid.
* In the lower left hand area of the panel you'll see the scale factor, move the cursor until the scale factor is 1.5000. 
Holding down the (key|ctrl) key will snap the scale factor to 0.1 units at a time, making 1.5000 easy.
* Click the left mouse button ((key|lmb)) to make the scale change.
* Still holding (key|ctrl) click-and-drag the plane using the right mouse button ((key|rmb)) 
until the lower left hand corner of the plane is at the axis. This is where the red and green lines cross.
* Left click ((key|lmb)) to move the plane to it's new position.

<center>This is how  you're plane should look at this point:</center>
<a href="/images/heightmaps-blender-05-movedplane.png"><img src="/images/heightmaps-blender-05-movedplane.png"></a>

### Making the height Gradient

ok, now it gets trickier.

#### Add a Material

<a href="/images/heightmaps-blender-06-materials.png"><img src="/images/heightmaps-blender-06-materials.png"></a>

* Open the <code>Material</code> Panel, to do this:
** click on <code>shading</code>
** then the materials button
* click on the <code>Add New</code> Button to add a new material
* under the <code>material</code> tab click on <code>Shadeless</code> button


### Add a Texture

#### Texture Tab

<div class="floatright">
    <a href="/images/heightmaps-blender-07-textures.png" class="image">
        <img alt="Texturetab.png" src="/images/heightmaps-blender-07-textures.png" width="277" height="231" /></a></div>
<ol><li>Open the <code>Texture</code> Panel
<ol><li>click on <code>shading</code>
</li><li>then the <code>texture</code> button
</li></ol>
</li><li>click on the <code>Add New</code> button to add a texture.
<ul><li>to change the name of the texture click on <code>Tex.001</code> and type in a new name, in our case <code>height</code>would be appropriate
</li></ul>
</li><li>Next, select <code>Blend</code> from the <code>Texture Type</code> "pulldown" menu.
</li></ol>
<div style="clear:both;"></div>

#### Colors Tab

<div class="floatright">
    <a href="/images/heightmaps-blender-08-colors.png" class="image">
        <img alt="Colortab.png" src="/images/heightmaps-blender-08-colors.png" width="281" height="199" /></a></div>
<ol><li>Go under the color tab and click on the <code>Colorband</code> button.
</li><li>There is a Field labeled<code>A</code> with a value of <code>0.000</code>, change the value to <code>1.000</code>
</li><li>Select the second color point by clicking on the white vertical band on the right of the colorband.
</li><li>change the color of the second colorpoint to white by making the <code>R</code> value <code>1.000</code>
</li></ol>
<div style="clear:both;"></div>

#### Mapping the texture

<div class="floatright">
    <a href="/images/heightmaps-blender-09-mapping.png" class="image">
        <img alt="Mapinputtab.png" src="/images/heightmaps-blender-09-mapping.png" width="280" height="199" /></a></div>
<ol><li>Now go back to the Materials
</li><li>under the Texture Tab make sure there is a check next to the name of the texture you just added.
</li><li>go into the <code>Map Input</code> tab
</li><li>in the lower left of this tab you'll see the mappings, select Z for all of mappings
</li></ol>
<div style="clear:both;"></div>
<p><br />
Cricky this is taking a long time to write!! but at least the texture is done now.
</p><p><br />
</p>

## Making the Camera

<div class="floatright">
    <a href="/images/heightmaps-blender-10-camera.png" class="image">
        <img alt="Camertab.png" src="/images/heightmaps-blender-10-camera.png" width="281" height="203" /></a></div>
<ol><li>Go back into <code>Object Mode</code> (<img  src="/images/blender-old-objectmode.png" width="132" height="25" /></a>)
</li><li>Under the View menu select <code>View</code> select <code>View Properties</code>
</li><li>Under <code>3D Cursor</code> change the <code>x</code>, <code>y</code>, <code>z</code> values to <code>1.50</code>, <code>1.50</code>, <code>5.00</code>.
</li><li>press <code><b>spacebar</b></code> and select <code>Add</code> -&gt; <code>Camera</code>
</li><li>hit (key|f9) or click the <code>editing</code> button to and you'll see a camera tab.
</li><li>click the <code>Orthographic</code> button
</li><li>change the value of scale to 3.00
</li></ol>
<div style="clear:both;"></div>

## Setting up the rendering

<div class="floatright">
    <a href="/images/heightmaps-blender-11-format.png" class="image">
        <img alt="Formattab.png" src="/images/heightmaps-blender-11-format.png" width="278" height="203" /></a></div>
<ol><li>press <code><b>f10</b></code> to enter the scene panel
</li><li>below the format tab change <code>SizeX</code>, and <code>SizeY</code> to <code>1025</code>
</li><li>under that, there is a menu for the formats, it defaults <code>Jpeg</code>. click on this pulldown and select <code>OpenEXR</code>
</li><li>select the <code>BW</code> button below that
</li></ol>
<p>Phew!! good news is that at this point everything is basically set up! Save this file so you can use it as a starting point for future terrains.
</p><p>For the lazy that just want to skip to this point here is a blender file saved at this point. <a href="/rorwikibackup/index.php?title=Special:Upload&amp;wpDestFile=Terntemplate.blend" class="new" title="Terntemplate.blend">Media:terntemplate.blend</a>
</p>

#### Test Render

since everything is set up at this point lets do a test render. simply press <code><b>f12</b></code> if a window pops up with some stats int he top with a gray image in the middle everything is working as it should.

## Making Terrain

<ol><li>Make sure you're in <code>Object Mode</code> (<img  src="/images/blender-old-objectmode.png" width="132" height="25" />)
</li><li>Right click on the plane you've created to select it
</li><li>Switch to <code>Edit Mode</code> (<img  src="/images/blender-old-editmode.png" width="137" height="24" />)
</li><li><div class="floatright">
    
    <img alt="Subdividemuti.png" src="/images/blender-old-subdivide.png" width="175" height="40" /></div>Press the <code><b>w</b></code> key and select <code>Subdivide Multi</code> from the menu
</li><li>The value entered in this box determined how many subdivisions each side is cut up into. 5 is good for demo purposes. you should now have a plane that looks like this:<br /><div class="center"><div class="floatnone">

    <a href="/images/heightmaps-blender-12-subdiv.png" class="image">
        <img alt="Subdividedplane.png" src="/images/heightmaps-blender-12-subdiv.png" width="409" height="403" /></a>

</div></div>
</li><li>rotate you're view by holding down the middle mouse button (<code><b>mmb</b></code>) and moving the mouse. move the view to a point where you can easily distinguish all 3 axis.
<ul><li>Alternatively, you can rotate the view using the keypad numbers <code><b>numpad 4</b></code>, <code><b>numpad 8</b></code>, <code><b>numpad 3</b></code>, and <code><b>numpad 2</b></code>
</li></ul>
</li><li>Right click on a vertex (these are the pink dots) to select it.
</li><li>Then click-and-drag the blue array pointing, this is you're z axis and by doing this you move the selected nodes along that one axis.
</li><li>You should end up with a picture similar to this:<br /><div class="center"><div class="floatnone">

    <a href="/images/heightmaps-blender-13-hill.png" class="image">
        <img alt="Singlehill.png" src="/images/heightmaps-blender-13-hill.png" width="441" height="360" /></a></div></div>
</li></ol>
<p>You now have a (Very) basic hill.
</p>

## Generating the heightmap

### Render the scene

<ol><li>Press <code><b>f12</b></code> to bring up the render window:
</li><li>Now press <code><b>f3</b></code> to bring up the save dialog, save this to a file with the extension of <code>.exr</code>. I saved it to <code>mymap.exr</code> for this tutorial.
</li></ol>
<p><br />
Instead of saving the image as .exr save it as .jpeg
</p>

### Convert to raw format

<p>Note: this process can vary depending on the platform.
</p>
<ol><li>open a command line and navigate to where the saved <code>.exr</code> file is saved.
</li><li>execute the following:<pre>convert mymap.exr -depth 16 -size 1025x1025 -endian LSB gray:mymap.raw</pre>
</li><li>Setup the <code>.tern</code> and <code>.cfg</code> as described in <a href="/rorwikibackup/index.php/Terrain_Formats" title="Terrain Formats">Terrain Formats</a>.
</li></ol>
<p>whola! the resulting file is a usable heightmap for RoR.
</p><p>This is the resulting image for the heightmap, your's should look somewhat similar:
</p>
<div class="center"><div class="floatnone">
    <a href="/images/heightmaps-blender-14-rendered.png" class="image">
        <img alt="Renderedplane.png" src="/images/heightmaps-blender-14-rendered.png" width="512" height="512" /></a></div></div>
<div style="clear:both;"></div>

You don't have to do this if you saved the image as a .jpeg
</p><p>you can import this in L3DT as a heightmap and export it as .raw
</p><p>Refer to the L3DT tutorial for details on how to size and export
</p>

## Where to go from here

<p>Well there are all kinds of guides on making terrains, some tools for it too.
</p><p>These are the resources I used to make this tutorial.<br />
<a rel="nofollow" class="external text" href="http://wiki.blender.org/index.php/Tutorials/Creating_a_Heightmap_from_a_Plane">Creating a Heightmap from a Plane</a><br />
<a rel="nofollow" class="external text" href="http://en.wikibooks.org/wiki/Blender_3D:_Noob_to_Pro/Mountains_Out_Of_Molehills">Mountains Out Of Molehills</a><br />
<a rel="nofollow" class="external text" href="http://en.wikibooks.org/wiki/Blender_3D:_Noob_to_Pro/Making_Landscapes_with_heightmaps">Making Landscapes with heightmaps</a><br />
<a rel="nofollow" class="external text" href="http://innerworld.sourceforge.net/index.html">InnerWorld terrain generator</a><br />
</p><p>In particular if you want to learn more general blender I highly suggest reading the <a rel="nofollow" class="external text" href="http://en.wikibooks.org/wiki/Blender_3D:_Noob_to_Pro">Blender 3D: Noob to Pro</a> book on wikibook.
</p>

## Troubleshooting

**Heightmap isn't the proper size**

Make sure the X and Y size of the render is <code>1025x1025</code>.
