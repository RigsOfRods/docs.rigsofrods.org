Making custom HUD
============


## Fundamental Concepts

The GUI is described in a Layout file (*.layout). It is an XML file format.

The Layout Files should be edited by the provided GUI Editor

The GUI is <i>linked</i> with RoR over "User Data" Strings. 
These are Strings that can be set-up in the LayoutEditors Widget Properties. 
A link is a connection between the GUI Elements and RoR game values.

The controls are separated via Layers, so they can overlap each other in a defined way:
<a href="/images/custom-hud-layers.png"><img src="/images/custom-hud-layers.png" width="355" height="92"  /></a>

Needles should go on top (<i>Main</i> Layer), static background images to the bottom (<i>Back</i> Layer)

## Required Software

<a rel="nofollow" class="external text" href="http://sourceforge.net/projects/rigsofrods/files/rigsofrods/0.38-dev/MyGUI_Tools_4.zip/download"
    >Gui Editor 4</a>
    
(old version: <a rel="nofollow" class="external text" 
    href="http://sourceforge.net/projects/rigsofrods/files/rigsofrods/0.38-dev/MyGUI_Tools_2.zip/download">GUI Editor 2</a>)

NOTE: some animations will not work exactly like in RoR yet. We are working on fixing this.

## Workflow

1. Create graphics of gauges and needles
2. Start GUIEditor and create the controls using your graphics 
3. Save the .layout and image files in your truck zip and use [`guisettings`](/vehicle-creation/fileformat-truck#guisettings) to integrate it with your vehicle.
4. Test in RoR and fix in GUIEditor

## Available animations

<!--
<td><b>Animation</b></td>
<td><b>Type / Values / Ranges</b></td>
<td><b>Load on FPS</b></td>
<td><b>Arguments</b></td>
<td><b>MyGUI Control to use</b></td> -->

### rotate

<img src="/images/custom-hud-anim-rotate.png">

Rotates a single image around its center

* Input type: float (real number)
* FPS impact: light
* Internals: based on MyGUI control 'RotatingSkin'

<img src="/images/custom-hud-gauge.png">

Arguments:

* <b>min</b> - the minimum rotation angle
* <b>max</b> - the maximum rotation angle
* <b>vmin</b> - the value at the minimum angle
* <b>vmax</b> - the value at the maximum angle

Example for a simple speedo gauge:

```
anim=rotate
min=-104
max=110
vmin=0
vmax=120
link=speedo_kph
```

### lamp

Switches between two images

<img src="/images/custom-hud-anim-lamp.png">

* Input type: boolean (true/false)
* FPS impact: light
* Internals: based on MyGUI control 'ImageBox'

Arguments:

* <b>texture</b> - the basename of the texture to use<br>
The resulting images are called [texture]-on.png and [texture]-off.png

Example for a simple clutch lamp (images are clutch-on.png and clutch-off.png):

```
anim=lamp
texture=clutch
link=clutchLamp
``` 

Lamps can have conditions on when they switch states. 
Currently there is only support for &lt; and &gt; comparisons. 
For example this lamp will be "on" for speeds over 50kph:

```
anim=lamp
texture=clutch
link=speedo_kph&gt;50
```

### series

Switches between N images

<img src="/images/custom-hud-anim-series.png">

* Input type: integer (whole number)
* FPS impact: light
* Internals: based on MyGUI control 'ImageBox'

Arguments:

* <b>texture</b> - the basename of the texture to use<br>
The resulting images are called &lt;texture&gt;-&lt;number&gt;.png

Example for a simple secured lamp (images are secured-0.png, secured-1.png and secured-2.png):

```
anim=series
texture=secured
link=ties_mode
```

### scale

Scales one image

<img src="/images/custom-hud-anim-scale.png">

* Input type: float (real number)
* FPS impact: heavier
* Internals: based on MyGUI control 'ImageBox'

Arguments:

* <b>min</b> - the minimum size to add</li>
* <b>max</b> - the maximum size to add</li>
* <b>vmin</b> - the value at the minimum size</li>
* <b>vmax</b> - the value at the maximum size</li>
* <b>direction</b> - what side to scale up. possible values:
 up, down, left, right
 
Example for a simple speedo bar (which is 200 pixels width):

```
anim=scale
min=-200
max=0
vmin=0
vmax=120
direction=right
link=speedo_kph
```

### translate

Moves around one image

<img src="/images/custom-hud-anim-translate.png">

* Input type: float (real number)
* FPS impact: heavier
* Internals: based on MyGUI control 'ImageBox'

Arguments:

* <b>min</b> - the minimum size to translate
* <b>max</b> - the maximum size to translate
* <b>vmin</b> - the value at the minimum translation
* <b>vmax</b> - the value at the maximum translation
* <b>direction</b> - what side to move to. possible values:
 up, down, left, right
 
Example for a simple speedo bar:

```
anim=translate
min=0
max=200
vmin=0
vmax=120
direction=right
link=speedo_kph
```

### textstring / textformat

Displays text

<img src="/images/custom-hud-anim-text.png">

* Input type: text (max 250 characters)
* FPS impact: light
* Internals: based on MyGUI control 'TextBox'

Arguments:

* <b>format</b> - (optional) the display format that should be used, 
see <a rel="nofollow" class="external text" href="http://www.cplusplus.com/reference/clibrary/cstdio/printf/">here for more info</a>.

Example for a simple speedo display:

```
anim= textstring or textformat
format=%04.0f km/h
link=speedo_kph
```

## Input sources

Color code represents the input type

<table border="1">
<tr>
<td><b>Link-Name</b></td>
<td><b>Description</b></td>
<td><b>Type / Values / Ranges</b></td>
<td><b>Active when</b></td>
</tr>

<tr style="background-color:#ddffff">
<td><b>rpm</b></td>
<td>Engine RPM</td>
<td>Float: 0 - max truck RPM</td>
<td>Engine exists</td>
</tr>

<tr style="background-color:#ddffff">
<td><b>speedo_kph</b></td>
<td>Wheel Speed in kilometer per hour</td>
<td>Float: unlimited, minus if driving backwards</td>
<td>Always</td>
</tr>

<tr style="background-color:#ddffff">
<td><b>speedo_mph</b></td>
<td>Wheel Speed in miles per hour</td>
<td>Float: unlimited, minus if driving backwards</td>
<td>Always</td>
</tr>

<tr style="background-color:#ddffff">
<td><b>engine_turbo</b></td>
<td>Engines Turbo PSI value</td>
<td>Float: unlimited</td>
<td>Engine exists</td>
</tr>

<tr style="background-color:#ffddff">
<td><b>engine_ignition</b></td>
<td><i>true</i> if engine has contact, <i>false</i> if not</td>
<td>Boolean: true or false</td>
<td>Engine exists</td>
</tr>

<tr style="background-color:#ffddff">
<td><b>engine_battery</b></td>
<td><i>true</i> if engine has contact and is nor running, <i>false</i> if not</td>
<td>Boolean: true or false</td>
<td>Engine exists</td>
</tr>

<tr style="background-color:#ffddff">
<td><b>engine_clutch_warning</b></td>
<td><i>true</i> if engine torque is greater than the clutch force, <i>false</i> if not</td>
<td>Boolean: true or false</td>
<td>Engine exists</td>
</tr>

<tr style="background-color:#ffffdd">
<td><b>engine_gear</b></td>
<td>Gear number, negative for reverse</td>
<td>Integer: -1 for first reverse gear, 0 for neutral, 1 for first gear, etc</td>
<td>Engine exists</td>
</tr>

<tr style="background-color:#ffffdd">
<td><b>engine_num_gear</b></td>
<td>Number of available gears, does not change</td>
<td>Integer: i.e. 6 for six usable gears</td>
<td>Engine exists</td>
</tr>

<tr style="background-color:#ddffdd">
<td><b>engine_gear_string</b></td>
<td>String that shows the gears in relation to the number of gears</td>
<td>Character: "&lt;current gear&gt; / &lt;num gears&gt;" or "N" or "R"</td>
<td>Engine exists</td>
</tr>

<tr style="background-color:#ffffdd">
<td><b>engine_auto_gear</b></td>
<td>Automatic gear (R/N/D/1/2)</td>
<td>Integer: same as gear but for automatic</td>
<td>Engine exists</td>
</tr>

<tr style="background-color:#ddffff">
<td><b>engine_clutch</b></td>
<td>Current clutch value</td>
<td>Float: 0 (not pressed) to 1 (fully pressed down)</td>
<td>Engine exists</td>
</tr>

<tr style="background-color:#ddffff">
<td><b>brake</b></td>
<td>Current brake value</td>
<td>Float: 0 (not pressed) to 1 (fully pressed down)</td>
<td>Always</td>
</tr>

<tr style="background-color:#ddffff">
<td><b>accelerator</b></td>
<td>Current accelerator value</td>
<td>Float: 0 (not pressed) to 1 (fully pressed down)</td>
<td>Engine exists</td>
</tr>

<tr style="background-color:#ddffff">
<td><b>roll</b></td>
<td>Current cabin roll - values represents angle in degree</td>
<td>Float: unlimited</td>
<td>Always</td>
</tr>

<tr style="background-color:#ddffff">
<td><b>roll_corr</b></td>
<td>Current cabin roll targeted by active shocks - values represents angle in degree</td>
<td>Float: unlimited</td>
<td>Always</td>
</tr>

<tr style="background-color:#ffddff">
<td><b>roll_corr_active</b></td>
<td><i>true</i> when the active shocks are working</td>
<td>Boolean: true/false</td>
<td>Always</td>
</tr>

<tr style="background-color:#ddffff">
<td><b>pitch</b></td>
<td>Current cabin pitch - values represents angle in degree</td>
<td>Float: unlimited</td>
<td>Always</td>
</tr>


<tr style="background-color:#ffddff">
<td><b>parkingbrake</b></td>
<td><i>true</i> if parking brake is on</td>
<td>Boolean: true/false</td>
<td>Always</td>
</tr>

<tr style="background-color:#ffddff">
<td><b>locked</b></td>
<td><i>true</i> if any hooks are locked to something</td>
<td>Boolean: true/false</td>
<td>Always</td>
</tr>

<tr style="background-color:#ffddff">
<td><b>low_pressure</b></td>
<td><i>true</i> if hydraulics cannot work as the RPM is too low</td>
<td>Boolean: true/false</td>
<td>Always</td>
</tr>

<tr style="background-color:#ffddff">
<td><b>lights</b></td>
<td><i>true</i> if headlights are on</td>
<td>Boolean: true/false</td>
<td>Always</td>
</tr>

<tr style="background-color:#ffffdd">
<td><b>tractioncontrol_mode</b></td>
<td>TractionControl (TC) mode</td>
<td>Integer: 0-3: 0 = not present, 1 = off, 2 = on, 3 = active</td>
<td>Always</td>
</tr>

<tr style="background-color:#ffffdd">
<td><b>antilockbrake_mode</b></td>
<td>Anti Lock Brake (ALB) mode</td>
<td>Integer: 0-3: 0 = not present, 1 = off, 2 = on, 3 = active</td>
<td>Always</td>
</tr>

<tr style="background-color:#ffffdd">
<td><b>ties_mode</b></td>
<td>Ties locking state</td>
<td>Integer: 0-2: 0 = not tied, 1 = prelock (currently tightening), 2 = tied (locked)</td>
<td>Always</td>
</tr>

<tr style="background-color:#ddffff">
<td><b>screw_throttle_X</b></td>
<td>Boat Screw Throttle. X from 0 to 5 (DD_MAX_SCREWPROP)</td>
<td>Float: unlimited</td>
<td>Screwprop exists</td>
</tr>

<tr style="background-color:#ddffff">
<td><b>screw_steer_X</b></td>
<td>Boat Screw Steering direction. X from 0 to 5 (DD_MAX_SCREWPROP)</td>
<td>Float: unlimited, -1 = left, +1 = right?</td>
<td>Screwprop exists</td>
</tr>

<tr style="background-color:#ddffff">
<td><b>water_depth</b></td>
<td>Depth of water below lowest node</td>
<td>Float: unlimited</td>
<td>Screwprop exists</td>
</tr>

<tr style="background-color:#ddffff">
<td><b>water_speed</b></td>
<td>Speed on water in knots (1 Nautical Mile/Hour)</td>
<td>Float: unlimited</td>
<td>Screwprop exists</td>
</tr>

<tr style="background-color:#ddffff">
<td><b>aeroengine_throttle_X</b></td>
<td>Airplane Engine Throttle. X from 0 to 5 (DD_MAX_AEROENGINE)</td>
<td>Float: 0-1</td>
<td>Aeroengine exists</td>
</tr>

<tr style="background-color:#ffddff">
<td><b>aeroengine_failed_X</b></td>
<td>Airplane Engine Failure. X from 0 to 5 (DD_MAX_AEROENGINE)</td>
<td>Boolean: true if failed</td>
<td>Aeroengine exists</td>
</tr>

<tr style="background-color:#ddffff">
<td><b>aeroengine_rpm_X</b></td>
<td>Airplane Engine RPM. X from 0 to 5 (DD_MAX_AEROENGINE)</td>
<td>Float: 0 to aeroengine max RPM</td>
<td>Aeroengine exists</td>
</tr>

<tr style="background-color:#ddffff">
<td><b>airspeed</b></td>
<td>Speed above ground in knots/hour</td>
<td>Float: unlimited</td>
<td>Aeroengine or wing exists</td>
</tr>

<tr style="background-color:#ddffff">
<td><b>wing_aoa_X</b></td>
<td>Wings Angle of Attack. X from 0 to 5 (DD_MAX_WING)</td>
<td>Float: unlimited</td>
<td>Wing exists</td>
</tr>

<tr style="background-color:#ddffff">
<td><b>altitude</b></td>
<td>Altitude above ground</td>
<td>Float: unlimited</td>
<td>Aeroengine or wing exists</td>
</tr>

<tr style="background-color:#ddffdd">
<td><b>altitude_string</b></td>
<td>Altitude above ground - string</td>
<td>Characters: three character altitude display: "000"</td>
<td>Aeroengine or wing exists</td>
</tr>

<tr style="background-color:#dddddd">
<td><b>WORK IN PROGRESS</b></td>
<td>MORE TO COME....</td>
<td></td>
<td></td>
</tr>

</table>

## Quickstart

Perhaps the easiest thing to add is a text readout, here we will add a simple readout that shows the speed of a vehicle in MPH.

**1. Load up the layout editor and add a TextBox.**

You can do this by opening the Widgets tab, and under default you will find TextBox. Drag a TextBox out on the canvas as shown:

<img src="/images/custom-hud-quickstart-1.png" style="width: 100%">

**2. Change the properties of the TextBox.**

Do this in the Properties tab as shown. Align should be to a corner of the screen (Left Top here) and Layer should be "Main". Also add the user data properties:

```
anim=text
link=speedo_mph
```

put the keyword (e.g. "anim") into the box above "Key" and put the value (e.g. "text") above the box marked "Value." 
Then click on "Add" and repeat this step for all the user data properties. In the end you should have these properties for the TextBox:

<img src="/images/custom-hud-quickstart-2.png" style="width: 100%">

**3: Save the layout as "namehere.layout" and put the layout with the vehicle's .truck file.**

In the .truck file add the following lines:

```
guisettings
dashboard namehere.layout
```

**4: Test your readout!**

Extra: Add these user values to format the display like this: "xxxx.xx MPH"

```
format=%.2f MPH
```

Now you have the basics of the layouteditor, move on to more advanced readouts. Let's now create a simple speedo gauge:

**IMPORTANT:** Put your graphics into the YourMedia sub folder, so the editor can use it.

1. Open the layout editor.
2. Add an ImageBox in the same way that you added a TextBox in the first part of this quickstart.
3. Go into the ImageBox's properties and put the gauge texture into the ImageTexture field.
4. Add a RotatingSkin widget  add your needle texture to it in the same way as you did previously.
5. Add these values to the RotatingSkin as User data:
```
anim=rotate
min=-104
max=110
vmin=0
vmax=120
link=speedo_kph
```
6. Save your .layout file, and move it and the images to your truck folder, and add the truck&lt;--&gt;.layout linkage 
 as you did earlier in the quickstart.
7. Test out your gauge, and make modifications as necessary.

