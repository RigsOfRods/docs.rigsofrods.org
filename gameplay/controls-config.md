---
layout: page
title:  "Controls and configuration"
categories: [gameplay]
---

# Intro

Rigs of Rods is a simulator which strives for maximum reallism, and hence you need an appropriate controller, such as a wheel for land vehicles and joystick for aerial or marine vehicles.

Input is configured using configuration file 'input.map'. It's also possible to configure them via our 'configurator' utility, RoRConfig. In-game configuration of controls is not implemented yet.

# Keyboard layout

## General keys

![](/images/input-map-general.png) 

<table style="color: #ab7e3a; display: inline-block; vertical-align: top;">
    <tr><th>Misc</th><th>Key</th></tr>

    <tr><td>Enter or exit truck</td><td>ENTER   </td></tr>
    <tr><td>Quit Game          </td><td>ESC     </td></tr>
    <tr><td>Toggle Statistics  </td><td>T       </td></tr>
    <tr><td>Screenshot         </td><td>PRINTSCR</td></tr>
    <tr><td>chat (Multiplayer) </td><td>Y       </td></tr>
</table>

<table style="color: #127220; display: inline-block; vertical-align: top;">
    <tr><th>Character control</th><th>Key</th></tr>

    <tr><td>Jump          </td><td>SPACE   </td></tr>
    <tr><td>Turn Right    </td><td>RIGHT   </td></tr>
    <tr><td>Turn Left     </td><td>LEFT    </td></tr>
    <tr><td>Walk Fordwards</td><td>UP      </td></tr>
    <tr><td>Walk Backwards</td><td>DOWN    </td></tr>
    <tr><td>Run           </td><td>SHIFT+UP</td></tr>
</table>

<table style="display: inline-block; vertical-align: top;">
    <tr>
        <th><span style="color: #6692b3">Camera</span> / <span style="color: #ced925">Caelum</span></th>
        <th>Key</th>
    </tr>
    <!--camera-->
    <tr><td style="color: #6692b3">Change        </td><td style="color: #6692b3">C                     </td></tr>
    <tr><td style="color: #6692b3">control camera</td><td style="color: #6692b3">1, 2, 3, 4, 5, 6, 8, 9</td></tr>
    <!--caelum-->
    <tr><td style="color: #ced925">Increase time</td><td style="color: #ced925">+</td></tr>
    <tr><td style="color: #ced925">Decrease time</td><td style="color: #ced925">-</td></tr>
</table>

## Land vehicle keys

![](/images/input-map-truck.png) 

<table style="display: inline-block; vertical-align: top;">
    <tr><th>Drive controls</th><th>Key</th></tr>
    
    <!--Truck control-->
    <tr><td style="color: #127220">Steer Left                               </td><td style="color: #127220">LEFT     </td></tr>
    <tr><td style="color: #127220">Steer Right                              </td><td style="color: #127220">RIGHT    </td></tr>
    <tr><td style="color: #127220">Accelerate/Brake                         </td><td style="color: #127220">UP / DOWN</td></tr>
    <tr><td style="color: #127220">Tire Pressure +/-<br>(not for all trucks)</td><td style="color: #127220">[ ]      </td></tr>
    
    <!--Gear / clutch-->
    <tr><td style="color: #ced925">Autoshift Up      </td><td style="color: #ced925">PAGE-UP  </td></tr>
    <tr><td style="color: #ced925">Autoshift Down    </td><td style="color: #ced925">PAGE-DOWN</td></tr>
    <tr><td style="color: #ced925">Switch Shift Modes</td><td style="color: #ced925">Q        </td></tr>
    <tr><td style="color: #ced925">Manual Clutch     </td><td style="color: #ced925">SHIFT    </td></tr>
    <tr><td style="color: #ced925">Shift Up          </td><td style="color: #ced925">A        </td></tr>
    <tr><td style="color: #ced925">Shift Down        </td><td style="color: #ced925">Z        </td></tr>
</table>

<table style="color: #ab7e3a; display: inline-block; vertical-align: top;">
    <tr><th>Misc</th><th>Key</th></tr>

    <tr><td>Truck Horn        </td><td>H     </td></tr>
    <tr><td>Parking Brake     </td><td>P     </td></tr>
    <tr><td>Blinker Left      </td><td>COMMA </td></tr>
    <tr><td>blinker Right     </td><td>DOT   </td></tr>
    <tr><td>Blink Warn        </td><td>PERIOD</td></tr>
    <tr><td>Toggle Contact    </td><td>X     </td></tr>
    <tr><td>Starter           </td><td>S     </td></tr>
    <tr><td>Lock Load         </td><td>L     </td></tr>
    <tr><td>Secure Load       </td><td>O     </td></tr>
    <tr><td>Reset Truck       </td><td>I     </td></tr>
    <tr><td>Show Skeleton     </td><td>K     </td></tr>
    <tr><td>Toggle Lights     </td><td>N     </td></tr>
    <tr><td>Toggle beacons    </td><td>M     </td></tr>
    <tr><td>Rescue Truck      </td><td>R     </td></tr>
    <tr><td>Toggle HUD        </td><td>U     </td></tr>
    <tr><td>Enter / Exit truck</td><td>ENTER </td></tr>
    <tr><td>particle Cannon   </td><td>G     </td></tr>
</table>

<table style="color: red; display: inline-block; vertical-align: top;">
    <tr><th>Function keys</th><th>Combo</th></tr>
    
    <tr><td>COMMANDS 01</td><td>F1</td></tr>
    <tr><td>...</td><td>...</td></tr>
    <tr><td>COMMANDS 12</td><td>F12</td></tr>
    <tr><td>COMMANDS 13</td><td>CTRL + F1</td></tr>
    <tr><td>...</td><td>...</td></tr>
    <tr><td>COMMANDS 24</td><td>CTRL + F12</td></tr>
    <tr><td>COMMANDS 25</td><td>ALT + F1</td></tr>
    <tr><td>...</td><td>...</td></tr>
    <tr><td>COMMANDS 36</td><td>ALT + F12</td></tr>
    <tr><td>COMMANDS 37</td><td>CTRL + ALT + F1</td></tr>
    <tr><td>...</td><td>...</td></tr>
    <tr><td>COMMANDS 48</td><td>CTRL+ ALT + F12</td></tr>
	<tr><td>COMMANDS 49</td><td>CTRL+ SHIFT + F1</td></tr>
	<tr><td>...</td><td>...</td></tr>
	<tr><td>COMMANDS 58</td><td>CTRL + SHIFT + F10</td></tr>
	<tr><td>COMMANDS 59</td><td>CTRL + SHIFT + F11</td></tr>
	<tr><td>...</td><td>...</td></tr>
	<tr><td>COMMANDS 68</td><td>CTRL + ALT + F8</td></tr>	
	<tr><td>COMMANDS 69</td><td>CTRL + ALT + F9</td></tr>	
	<tr><td>...</td><td>...</td></tr>
	<tr><td>COMMANDS 78</td><td>CTRL + SHIFT + ALT + F6</td></tr>	
	<tr><td>COMMANDS 79</td><td>CTRL + SHIFT + ALT + F7</td></tr>	
	<tr><td>...</td><td>...</td></tr>
	<tr><td>COMMANDS 83</td><td>CTRL + SHIFT + ALT + F11</td></tr>	
	<tr><td>COMMANDS 84</td><td>CTRL + SHIFT + ALT + F12</td></tr>	
	

</table>

## Aerial and marine keys

![](/images/input-map-aerial-and-marine.png)

<table style="color: #127220; display: inline-block; vertical-align: top;">
    <tr><th>Airplane control</th><th>Key</th></tr>

    <tr><td>Steer Left   </td><td>LEFT              </td></tr>
    <tr><td>Steer Right  </td><td>RIGHT             </td></tr>
    <tr><td>Elevator Up  </td><td>UP                </td></tr>
    <tr><td>Elevator Down</td><td>DOWN              </td></tr>
    <tr><td>Rudder Right </td><td>X                 </td></tr>
    <tr><td>Rudder Left  </td><td>Z                 </td></tr>
    <tr><td>Brake        </td><td>B                 </td></tr>
    <tr><td>Parking Brake</td><td>P                 </td></tr>
    <tr><td>Reverse      </td><td>R                 </td></tr>
    <tr><td>Less Flaps   </td><td>1                 </td></tr>
    <tr><td>More Flaps   </td><td>2                 </td></tr>
    <tr><td>Throttle Down</td><td>PAGE-DOWN         </td></tr>
    <tr><td>Throttle Up  </td><td>PAGE-UP           </td></tr>
    <tr><td>Start Engines</td><td>CLICK BUTTONS "ON"</td></tr>
</table>

<table style="color: #ced925; display: inline-block; vertical-align: top;">
    <tr><th>Boat control</th><th>Key</th></tr>

    <tr><td>Throttle Down  </td><td>6    </td></tr>
    <tr><td>Throttle Up    </td><td>7    </td></tr>
    <tr><td>Steer Left     </td><td>LEFT </td></tr>
    <tr><td>Steer Right    </td><td>RIGHT</td></tr>
    <tr><td>Center Rudder  </td><td>DOWN </td></tr>
    <tr><td>Center Throttle</td><td>UP   </td></tr>
</table>

<table style="color: #ab7e3a; display: inline-block; vertical-align: top;">
    <tr><th>Misc</th><th>Key</th></tr>

    <tr><td>Parking Brake       </td><td>P    </td></tr>
    <tr><td>Lock Load           </td><td>L    </td></tr>
    <tr><td>Secure Load         </td><td>O    </td></tr>
    <tr><td>Reset Vehicle       </td><td>I    </td></tr>
    <tr><td>Show Skeleton       </td><td>K    </td></tr>
    <tr><td>Toggle Lights       </td><td>N    </td></tr>
    <tr><td>Toggle beacons      </td><td>M    </td></tr>
    <tr><td>Toggle HUD          </td><td>U    </td></tr>
    <tr><td>Enter / Exit vehicle</td><td>ENTER</td></tr>
</table>

It is recommended to use: - CTRL + HOME - to start all engine of a plane - CTRL + PGUP  - to full throttle all engines

because some planes could have more than 4 engines and you couldn't control them with your mouse.

# Config file 'input.map'

For all keys, see the [input.map](https://github.com/RigsOfRods/rigs-of-rods/blob/master/bin/resources/skeleton/config/input.map) file on GitHub.

This file defines all key alias for RoR. It has the following format:

    EVENT_NAME    EVENT_TYPE    MAPPING

For example:

    BOAT_CENTER_RUDDER     Keyboard    DOWN

This binds the <b>BOAT\_CENTER\_RUDDER</b> event to the <b>Down</b> arrow on your keyboard.

## Keyboard

For the keyboard there are several special things:

### Modifiers:
-   <b>CTRL</b>
-   <b>SHIFT</b>
-   <b>ALT</b>

Combine them with a + sign. Example:

    CAMERA_FREE_MODE    Keyboard    EXPL+SHIFT+C

### The EXPL tag

A special keyword used in defining commands.

In this example, only COMMANDS_01 is triggered when pressing F1, and COMMANDS_13 is triggered when pressing CTRL+F1 (but not COMMANDS_01)

    COMMANDS_01                    Keyboard             EXPL+F1 
    COMMANDS_13                    Keyboard             EXPL+CTRL+F1 

In this example, COMMANDS_01 would be triggered if you press CTRL+F1, as F1 is part of the COMMANDs_13 combination.

    COMMANDS_01                    Keyboard             F1 
    COMMANDS_13                    Keyboard             CTRL+F1 

### List of usable keys

0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, ABNT\_C1, ABNT\_C2, ADD, APOSTROPHE, APPS, AT, AX, B, BACK, BACKSLASH, C, CALCULATOR, CAPITAL, COLON, COMMA, CONVERT, D, DECIMAL, DELETE, DIVIDE, DOWN, E, END, EQUALS, ESCAPE, F, F1, F10, F11, F12, F13, F14, F15, F2, F3, F4, F5, F6, F7, F8, F9, G, GRAVE, H, HOME, I, INSERT, J, K, KANA, KANJI, L, LBRACKET, LCONTROL, LEFT, LMENU, LSHIFT, LWIN, M, MAIL, MEDIASELECT, MEDIASTOP, MINUS, MULTIPLY, MUTE, MYCOMPUTER, N, NEXTTRACK, NOCONVERT, NUMLOCK, NUMPAD0, NUMPAD1, NUMPAD2, NUMPAD3, NUMPAD4, NUMPAD5, NUMPAD6, NUMPAD7, NUMPAD8, NUMPAD9, NUMPADCOMMA, NUMPADENTER, NUMPADEQUALS, O, OEM\_102, P, PAUSE, PERIOD, PGDOWN, PGUP, PLAYPAUSE, POWER, PREVTRACK, Q, R, RBRACKET, RCONTROL, RETURN, RIGHT, RMENU, RSHIFT, RWIN, S, SCROLL, SEMICOLON, SLASH, SLEEP, SPACE, STOP, SUBTRACT, SYSRQ, T, TAB, U, UNDERLINE, UNLABELED, UP, V, VOLUMEDOWN, VOLUMEUP, W, WAKE, WEBBACK, WEBFAVORITES, WEBFORWARD, WEBHOME, WEBREFRESH, WEBSEARCH, WEBSTOP, X, Y, YEN, Z.

## Joystick, Wheel or gamepad

This category covers all analogue input devices detected by the operating system, so all gamepads, joysticks, wheels, pedals, etc.

### JoystickButton

Arguments:

-   <b>Joystick Number</b> (unused in modern mappings), set to 0
-   <b>Button number</b>

```
AIRPLANE_THROTTLE_DOWN    JoystickButton    0    2
```

### JoystickAxis

Arguments:

-   <b>Joystick Number</b> (unused in modern mappings), set to 0
-   <b>Axis number</b>
-   Options:
    -   <b>HALF</b>
    -   <b>REVERSE</b>
    -   <b>UPPER</b>
    -   <b>LOWER</b>
    -   <b>RELATIVE</b>
    -   <b>DIGITAL</b>
    -   <b>DEADZONE</b> : add deadzone in percent with equal sign: "DEADZONE=0.15".
    -   <b>LINEARITY</b>: add linearity in percent with equal sign: "LINEARITY=0.15".

```
AIRPLANE_STEER_RIGHT    JoystickAxis    0    1    UPPER+DEADZONE = 0.15
```

### JoystickPov

Arguments:

-   <b>Joystick Number</b> (unused in modern mappings), set to 0
-   <b>POV number</b>
-   Direction: <b>North</b>, <b>South</b>, <b>East</b>, <b>West</b>, <b>NorthEast</b>, <b>SouthEast</b>, <b>NorthWest</b>, <b>SouthWest</b>.


```
CHARACTER_FORWARD    JoystickPov    0    0    North
```

### JoystickSlider, JoystickSliderX, JoystickSliderY

Arguments:

-   <b>Joystick Number</b> (unused in modern mappings), set to 0
-   <b>Slider number</b>
-   Options:
    -   <b>REVERSE</b>

```
TRUCK_MANUAL_CLUTCH    JoystickSliderY    0    Y    0    REVERSE+DEADZONE = -30
```

Mouse
-----

Here is a simple tutorial/example, how to implement mouse control for Rigs of Rods.

You will need 2 applications:

-   vJoy joystick emulator:

<http://vjoystick.sourceforge.net/site/index.php/download-a-install/72-download>

-   FreePIE input emulator:

<http://andersmalmgren.github.io/FreePIE/index.html>

After installing these you have to edit your input map and define there joystick axises/buttons for the things you want to control with mouse.
Input map is located in: <b>Documents/Rigs of Rods 0.xx/config</b> and open a file called <b>Input.map</b>.
 I use mouse to control steering and throttle but I suppose you could use it to control anything you want. Add these lines in the input.map to get steering and throttle control: 
 
    TRUCK_ACCELERATE    JoystickAxis    0    1    LOWER
    TRUCK_BRAKE         JoystickAxis    0    1    UPPER
    TRUCK_STEER_LEFT    JoystickAxis    0    0    LOWER + DEADZONE = 0.00
    TRUCK_STEER_RIGHT   JoystickAxis    0    0    UPPER + DEADZONE = 0.00

Then you will need a python script for the FreePIE:

```
from System import Int16

if (starting):
    mousex = 0
    mousey = 0
    xlimit = 15600
    ylimit = 15600

mousex = mousex + (mouse.deltaX \* 40) mousey = mousey + (mouse.deltaY \* 80)

if (mouse.middleButton):
    mousex = 0
    mousey = 0

if (mousex >  xlimit): mousex =  xlimit
if (mousex < -xlimit): mousex = -xlimit
if (mousey >  ylimit): mousey =  ylimit
if (mousey < -ylimit): mousey = -ylimit

vJoy[0].x = mousex
vJoy[0].y = mousey

diagnostics.watch(vJoy[0].x)
diagnostics.watch(vJoy[0].y)
```

Open FreePIE, paste the script above in the code area and save the script.

For the mouse input to function, you have to run the script in FreePIE. Click Script -&gt; Run script. Leave it running, open RoR and start playing.

You can modify both the script and the input map to make them better suit for your use. For example the numbers 40 and 80 in the script are the sensitivity of the controls.

Mouse middle button in the script above, will reset the axises in game, in this case the steering and throttle.

%%%%%%%%%%%%%%%%%% old keypress events \#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#\#

**Keypress event identification in RoR 0.37.70+**
 These can be used as event option for prop animations.( add\_animation ), not all make sense though for animated props.
 AIRPLANE\_STEER\_RIGHT
AIRPLANE\_BRAKE
AIRPLANE\_ELEVATOR\_DOWN
AIRPLANE\_ELEVATOR\_UP
AIRPLANE\_FLAPS\_FULL
AIRPLANE\_FLAPS\_LESS
AIRPLANE\_FLAPS\_MORE
AIRPLANE\_FLAPS\_NONE
AIRPLANE\_PARKING\_BRAKE
AIRPLANE\_REVERSE
AIRPLANE\_RUDDER\_LEFT
AIRPLANE\_RUDDER\_RIGHT
AIRPLANE\_STEER\_LEFT
AIRPLANE\_STEER\_RIGHT
AIRPLANE\_THROTTLE\_AXIS
AIRPLANE\_THROTTLE\_DOWN
AIRPLANE\_THROTTLE\_FULL
AIRPLANE\_THROTTLE\_NO
AIRPLANE\_THROTTLE\_UP
AIRPLANE\_TOGGLE\_ENGINES
BOAT\_CENTER\_RUDDER
BOAT\_REVERSE
BOAT\_STEER\_LEFT
BOAT\_STEER\_LEFT\_AXIS
BOAT\_STEER\_RIGHT
BOAT\_STEER\_RIGHT\_AXIS
BOAT\_THROTTLE\_AXIS
BOAT\_THROTTLE\_DOWN
BOAT\_THROTTLE\_UP
CAELUM\_DECREASE\_TIME
CAELUM\_DECREASE\_TIME\_FAST
CAELUM\_INCREASE\_TIME
CAELUM\_INCREASE\_TIME\_FAST
CAMERA\_CHANGE
CAMERA\_LOOKBACK
CAMERA\_RESET
CAMERA\_ROTATE\_DOWN
CAMERA\_ROTATE\_LEFT
CAMERA\_ROTATE\_RIGHT
CAMERA\_ROTATE\_UP
CAMERA\_ZOOM\_IN
CAMERA\_ZOOM\_IN\_FAST
CAMERA\_ZOOM\_OUT
CAMERA\_ZOOM\_OUT\_FAST
CHARACTER\_BACKWARDS
CHARACTER\_FORWARD
CHARACTER\_JUMP
CHARACTER\_LEFT
CHARACTER\_RIGHT
CHARACTER\_RUN
CHARACTER\_SIDESTEP\_LEFT
CHARACTER\_SIDESTEP\_RIGHT
COMMANDS\_01
COMMANDS\_02
COMMANDS\_03
COMMANDS\_04
COMMANDS\_05
COMMANDS\_06
COMMANDS\_07
COMMANDS\_08
COMMANDS\_09
COMMANDS\_10
COMMANDS\_11
COMMANDS\_12
COMMANDS\_13
COMMANDS\_14
COMMANDS\_15
COMMANDS\_16
COMMANDS\_17
COMMANDS\_18
COMMANDS\_19
COMMANDS\_20
COMMANDS\_21
COMMANDS\_22
COMMANDS\_23
COMMANDS\_24
COMMANDS\_25
COMMANDS\_26
COMMANDS\_27
COMMANDS\_28
COMMANDS\_29
COMMANDS\_30
COMMANDS\_31
COMMANDS\_32
COMMANDS\_33
COMMANDS\_34
COMMANDS\_35
COMMANDS\_36
COMMANDS\_37
COMMANDS\_38
COMMANDS\_39
COMMANDS\_40
COMMANDS\_41
COMMANDS\_42
COMMANDS\_43
COMMANDS\_44
COMMANDS\_45
COMMANDS\_46
COMMANDS\_47
COMMANDS\_48
COMMON\_CONSOLEDISPLAY
COMMON\_CONSOLEMODE
COMMON\_ENTER\_CHATMODE
COMMON\_SEND\_CHAT
COMMON\_ENTER\_OR\_EXIT\_TRUCK
COMMON\_HIDE\_GUI
COMMON\_LOCK
COMMON\_ROPELOCK
COMMON\_MAP\_ALPHA
COMMON\_OUTPUT\_POSITION
COMMON\_PRESSURE\_LESS
COMMON\_PRESSURE\_MORE
COMMON\_QUIT\_GAME
COMMON\_SHOW\_MENU
COMMON\_REPAIR\_TRUCK
COMMON\_RESCUE\_TRUCK
COMMON\_RESET\_TRUCK
COMMON\_SCREENSHOT
COMMON\_SCREENSHOT\_BIG
COMMON\_SAVE\_TERRAIN
COMMON\_SECURE\_LOAD
COMMON\_SHOW\_SKELETON
COMMON\_START\_TRUCK\_EDITOR
COMMON\_TOGGLE\_CUSTOM\_PARTICLES
COMMON\_TOGGLE\_MAT\_DEBUG
COMMON\_TOGGLE\_RENDER\_MODE
COMMON\_TOGGLE\_REPLAY\_MODE
COMMON\_TOGGLE\_STATS
COMMON\_TOGGLE\_TRUCK\_BEACONS
COMMON\_TOGGLE\_TRUCK\_LIGHTS
COMMON\_TRUCK\_INFO
COMMON\_VIEW\_MAP
COMMON\_FOV\_LESS
COMMON\_FOV\_MORE
GRASS\_LESS
GRASS\_MORE
GRASS\_MOST
GRASS\_NONE
GRASS\_SAVE
MAP\_IN
MAP\_INTERACTIVE\_TOGGLE
MAP\_OUT
MENU\_DOWN
MENU\_LEFT
MENU\_RIGHT
MENU\_SELECT
MENU\_UP
TERRAINEDITOR\_BUILT
TERRAINEDITOR\_PITCHBACKWARD
TERRAINEDITOR\_PITCHFOREWARD
TERRAINEDITOR\_ROTATELEFT
TERRAINEDITOR\_ROTATERIGHT
TERRAINEDITOR\_SELECTROAD
TERRAINEDITOR\_TOGGLEOBJECT
TERRAINEDITOR\_TOGGLEROADTYPE
TRUCK\_ACCELERATE
TRUCK\_AUTOSHIFT\_DOWN
TRUCK\_AUTOSHIFT\_UP
TRUCK\_BLINK\_LEFT
TRUCK\_BLINK\_RIGHT
TRUCK\_BLINK\_WARN
TRUCK\_BRAKE
TRUCK\_HORN
TRUCK\_LIGHTTOGGLE1
TRUCK\_LIGHTTOGGLE2
TRUCK\_LIGHTTOGGLE3
TRUCK\_LIGHTTOGGLE4
TRUCK\_LIGHTTOGGLE5
TRUCK\_LIGHTTOGGLE6
TRUCK\_LIGHTTOGGLE7
TRUCK\_LIGHTTOGGLE8
TRUCK\_LIGHTTOGGLE9
TRUCK\_LIGHTTOGGLE10
TRUCK\_MANUAL\_CLUTCH
TRUCK\_PARKING\_BRAKE
TRUCK\_SHIFT\_DOWN
TRUCK\_SHIFT\_NEUTRAL
TRUCK\_SHIFT\_UP
TRUCK\_SHIFT\_GEAR\_REVERSE
TRUCK\_SHIFT\_GEAR1
TRUCK\_SHIFT\_GEAR2
TRUCK\_SHIFT\_GEAR3
TRUCK\_SHIFT\_GEAR4
TRUCK\_SHIFT\_GEAR5
TRUCK\_SHIFT\_GEAR6
TRUCK\_SHIFT\_GEAR7
TRUCK\_SHIFT\_GEAR8
TRUCK\_SHIFT\_GEAR9
TRUCK\_SHIFT\_GEAR10
TRUCK\_SHIFT\_GEAR11
TRUCK\_SHIFT\_GEAR12
TRUCK\_SHIFT\_GEAR13
TRUCK\_SHIFT\_GEAR14
TRUCK\_SHIFT\_GEAR15
TRUCK\_SHIFT\_GEAR16
TRUCK\_SHIFT\_GEAR17
TRUCK\_SHIFT\_GEAR18
TRUCK\_SHIFT\_LOWRANGE
TRUCK\_SHIFT\_MIDRANGE
TRUCK\_SHIFT\_HIGHRANGE
TRUCK\_STARTER
TRUCK\_STEER\_LEFT
TRUCK\_STEER\_RIGHT
TRUCK\_SWITCH\_SHIFT\_MODES
TRUCK\_SWITCH\_SHIFT\_MODE
TRUCK\_TOGGLE\_AXLE\_LOC
TRUCK\_TOGGLE\_CONTAC
COMMON\_SHOWTRUCKTOOL
COMMON\_RELOAD\_ROADS
COMMON\_FULLSCREEN\_TOGGLE
CAMERA\_FREE\_MODE\_FIX
CAMERA\_FREE\_MODE
TRUCK\_LEFT\_MIRROR\_LEFT
TRUCK\_LEFT\_MIRROR\_RIGHT
TRUCK\_RIGHT\_MIRROR\_LEFT
TRUCK\_RIGHT\_MIRROR\_RIGHT
COMMON\_REPLAY\_FORWARD
COMMON\_REPLAY\_BACKWARD
COMMON\_REPLAY\_FAST\_FORWARD
COMMON\_REPLAY\_FAST\_BACKWARD
AIRPLANE\_AIRBRAKES\_NONE
AIRPLANE\_AIRBRAKES\_FULL
AIRPLANE\_AIRBRAKES\_LESS
AIRPLANE\_AIRBRAKES\_MORE
AIRPLANE\_THROTTLE
COMMON\_TRUCK\_REMOVE
COMMON\_NETCHATDISPLAY
COMMON\_NETCHATMODE
CHARACTER\_ROT\_UP
CHARACTER\_ROT\_DOWN
CHARACTER\_UP
CHARACTER\_DOWN
TRUCK\_SAVE\_POS1
TRUCK\_SAVE\_POS2
TRUCK\_SAVE\_POS3
TRUCK\_SAVE\_POS4
TRUCK\_SAVE\_POS5
TRUCK\_SAVE\_POS6
TRUCK\_SAVE\_POS7
TRUCK\_SAVE\_POS8
TRUCK\_SAVE\_POS9
TRUCK\_SAVE\_POS10
TRUCK\_LOAD\_POS1
TRUCK\_LOAD\_POS2
TRUCK\_LOAD\_POS3
TRUCK\_LOAD\_POS4
TRUCK\_LOAD\_POS5
TRUCK\_LOAD\_POS6
TRUCK\_LOAD\_POS7
TRUCK\_LOAD\_POS8
TRUCK\_LOAD\_POS9
TRUCK\_LOAD\_POS10
DOF\_TOGGLE
DOF\_DEBUG
DOF\_DEBUG\_TOGGLE\_FOCUS\_MODE
DOF\_DEBUG\_ZOOM\_IN
DOF\_DEBUG\_ZOOM\_OUT
DOF\_DEBUG\_APERTURE\_MORE
DOF\_DEBUG\_APERTURE\_LESS
DOF\_DEBUG\_FOCUS\_IN
DOF\_DEBUG\_FOCUS\_OUT

# Configuring controls with RoRConfig

1. Plug in your device, open the Configurator and go to the **"Controls"** tab.

![](/images/rorconfig-controls-tutorial-1.png)

2. Click the **"Add"** button.

![](/images/rorconfig-controls-tutorial-2.png)

3. In the box, choose an event from the top combo box, a description will appear below it, then choose an input type from the bottom combo box. (Keyboard, Joystick axis, Joystick button)

4. Click on **"Add"** and then press/move the button/axis you want to control the event.

![](/images/rorconfig-controls-tutorial-3.png)

5. Do step 4 for all the controls you want to map.

5. (Optional) Click the **"Test"** button, then press/move a mapped control to test the control, The top bar is the raw input from the button/axis, the lower bar is what the game "sees" after deadzone and linearity options have been applied.

6. Go test your control in the game! It may be a good idea to click on **"Export keymap"** to export your current keymap for later use.

# How to contribute input maps

1. Attach your wheel/joystick/gamepad that you want to map.

2. Download [Inputtool.zip](:Media:Inputtool3.zip "wikilink"). When you execute 'inputtool.exe' it will create a textfile named 'inputinfo.txt' in the same directory. This text file contains the relevant 'VendorMapFilename'.

3. Create a mapping file named like the value of 'VendorMapFilename' you just found out in the Rigs of Rods/config/ folder.

4. Improve and test the mapping by using RoR and a text editor. (see also [Input.map](Input.map "wikilink"))

-   Hint: You might find it easier to copy an [existing](http://www.rigsofrods.com/threads/96556-Joystick-specific-Input-maps) input map and edit commands to match your controller.

5. When you are finished with your configuration, copy and paste relevant infos from inputinfo.txt into your map file. Also make a comment (";" marks the rest of the line as a comment) after every command which button is used so others can easily see what button they have to use. See template:

``` text
;This is the input map for the Rigs of Rods game for the following device:
;
;"Xbox 360 Wireless Controller for Windows" by Microsoft
;
; created by Foobar in September 2012. 
;
;Joystick 1
;   Vendor: Controller (Xbox 360 Wireless Receiver for Windows)
;   VendorMapFilename: Controller__Xbox_360_Wireless_Receiver_for_Windows_.map
;   ID: 0
;   Type: [3] OISJoyStick
;   Axes: 5
;   Sliders: 0
;   POV/HATs: 1
;   Buttons: 10
;   Vector3: 0
;   Vector3Sensitivity: 2.28
;
;Control Overview:
;* Axis 1 (the up/down): accelerate/brake
;* Button 1 : (big red thing in the middle) : Horn
;...

; AIRPLANE
AIRPLANE_PARKING_BRAKE          JoystickButton       0 6 ;back
AIRPLANE_THROTTLE_DOWN          JoystickButton       0 2 ;X
AIRPLANE_THROTTLE_UP            JoystickButton       0 1 ;B
...
```

6. Submit <your map filename>.map as a new post [here](http://www.rigsofrods.com/threads/96556-Joystick-specific-Input-maps)

Thank you!

[Category:File Format](Category:File_Format "wikilink")
