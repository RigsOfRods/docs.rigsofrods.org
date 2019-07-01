---
layout: page
title:  "Controls and configuration"
categories: [gameplay]
---

<div class="toc" markdown="1">
  * TOC
  {:toc}
</div>

# Intro

Rigs of Rods is a simulator which strives for maximum reallism, and hence you need an appropriate controller, such as a wheel for land vehicles and joystick for aerial or marine vehicles.

Input is configured by editing configuration file [input.map](#config-file-inputmap) or by using the [Input Mapping Tool](#configuring-controls-with-the-input-mapping-tool). In-game configuration of controls is not implemented yet.

# Keyboard layout

<img src="/images/input-map-general.png" alt="General keyboard layout" width="600"/>

## General controls 

<table style="display: inline-block; vertical-align: top;">
	<tr bgcolor="#E5A36C"><th style="color: #000000">General</th><th style="color: #000000">Key</th></tr>
    <tr><td>Pause game            </td><td>ESC</td></tr>
    <tr><td>Quit game            </td><td>ALT+F4</td></tr>
	<tr><td>Spawn new vehicle</td><td>CTRL+G</td></tr>
    <tr><td>Enter or exit vehicle</td><td>ENTER</td></tr>
    <tr><td>Reset vehicle       </td><td>I    </td></tr>
    <tr><td>Reset vehicle in place</td><td>BACKSPACE</td></tr>
    <tr><td>View vehicle statistics </td><td>T</td></tr>
    <tr><td>View vehicle commands</td><td>CTRL+T</td></tr>
    <tr><td>Screenshot         </td><td>Print Screen/SYSRQ</td></tr>
    <tr><td>Chat (Multiplayer) </td><td>Y</td></tr>
    <tr><td>Toggle HUD          </td><td>U    </td></tr>
    <tr><td>Toggle soft reset mode</td><td>APOSTROPHE</td></tr>
    <tr><td>Toggle limited camera movement</td><td>SHIFT+SPACE</td></tr>
    <tr><td>Adjust simulation speed</td><td>CTRL+= / SHIFT+= </td></tr>
    <tr><td>Reset simulation speed/set preset</td><td>BACKSLASH</td></tr>
    <tr><td>Switch between vehicles </td><td>CTRL+RBRACKET / CTRL+LBRACKET </td></tr>
    <tr><td>Remove current vehicle</td><td>CTRL+Del</td></tr>
    <tr><td>Respawn last vehicle</td><td>CTRL+ . (period)</td></tr>
</table>

### Character 

<table style="display: inline-block; vertical-align: top;">
    <tr bgcolor="#5FAC5E"><th style="color: #000000">Character</th><th style="color: #000000">Key</th></tr>
    <tr><td>Jump          </td><td>SPACE   </td></tr>
    <tr><td>Turn right    </td><td>RIGHT   </td></tr>
    <tr><td>Turn left     </td><td>LEFT    </td></tr>
    <tr><td>Walk forwards </td><td>UP      </td></tr>
    <tr><td>Walk backwards</td><td>DOWN    </td></tr>
    <tr><td>Run           </td><td>SHIFT+UP</td></tr>
</table>

### Camera

<table style="display: inline-block; vertical-align: top;">
    <tr bgcolor="#74A9E1"><th style="color: #000000">Camera</th><th style="color: #000000">Key</th></tr>
    <tr><td>Change view        </td><td>C</td></tr>
    <tr><td>Rotate up/down     </td><td>Numpad 8 / Numpad 2</td></tr>
    <tr><td>Rotate left/right  </td><td>Numpad 4 / Numpad 6</td></tr>
    <tr><td>Zoom in/out        </td><td>Numpad 9 / Numpad 3</td></tr>
    <tr><td>Zoom in/out (fast) </td><td>SHIFT+Numpad 9 / SHIFT+Numpad 3</td></tr>
    <tr><td>Free camera   </td><td>SHIFT+C</td></tr>
    <tr><td>Fixed camera  </td><td>ALT+C</td></tr>
</table>

### Time
(Sky type must be set to Caelum or SkyX)
<table style="display: inline-block; vertical-align: top;">
    <tr bgcolor="#DFDD78"><th style="color: #000000">Time Adjust</th><th style="color: #000000">Key</th></tr>
    <tr><td>Change time        </td><td>Numpad + (plus) / Numpad - (minus)</td></tr>
    <tr><td>Change time (fast)</td><td>SHIFT+Numpad + (plus) / SHIFT+Numpad - (minus)</td></tr>
</table>

### Overview map

<table style="display: inline-block; vertical-align: top;">
    <tr bgcolor="#928578"><th style="color: #000000">Map</th><th style="color: #000000">Key</th></tr>
    <tr><td>Toggle map view </td><td>TAB</td></tr>
    <tr><td>Zoom in/out     </td><td>CTRL+TAB / SHIFT+TAB</td></tr>
    <tr><td>Toggle alpha     </td><td>CTRL+SHIFT+TAB</td></tr>
    <tr><td>Toggle icons     </td><td>CTRL+SHIFT+ALT+TAB</td></tr>
</table>

### Saves

<table style="display: inline-block; vertical-align: top;">
    <tr bgcolor="#928578"><th style="color: #000000">Savegames</th><th style="color: #000000">Key</th></tr>
    <tr><td>Quick save</td><td>NUMPAD / (divide)</td></tr>
    <tr><td>Quick load</td><td>NUMPAD * (multiply)</td></tr>
    <tr><td>Save slot 1</td><td>CTRL+ALT+1</td></tr>
    <tr><td>Save slot 2</td><td>CTRL+ALT+2</td></tr>
    <tr><td>Save slot 3</td><td>CTRL+ALT+3</td></tr>
    <tr><td>Save slot 4</td><td>CTRL+ALT+4</td></tr>
    <tr><td>Save slot 5</td><td>CTRL+ALT+5</td></tr>
    <tr><td>Load slot 1</td><td>ALT+1</td></tr>
    <tr><td>Load slot 2</td><td>ALT+2</td></tr>
    <tr><td>Load slot 3</td><td>ALT+3</td></tr>
    <tr><td>Load slot 4</td><td>ALT+4</td></tr>
    <tr><td>Load slot 5</td><td>ALT+5</td></tr>
</table>

Note: You can load a savegame from the main menu.

## Common vehicle controls

<img src="/images/input-map-truck.png" alt="Vehicle keyboard layout" width="600"/>

<table style="display: inline-block; vertical-align: top;">
    <tr bgcolor="#5FAC5E"><th style="color: #000000">Basic vehicle controls</th><th>Key</th></tr>
    <tr><td>Steer Left                               </td><td>LEFT     </td></tr>
    <tr><td>Steer Right                              </td><td>RIGHT    </td></tr>
    <tr><td>Accelerate/Brake                         </td><td>UP / DOWN</td></tr>
    <tr><td>Tire Pressure<br>(not for all trucks)</td><td>RBRACKET / LBRACKET</td></tr>
</table>

### Shifting

<table style="display: inline-block; vertical-align: top;">
    <tr bgcolor="#DFDD78"><th style="color: #000000">Shifting</th><th>Key</th></tr>
    <tr><td>Autoshift up      </td><td>PGUP  </td></tr>
    <tr><td>Autoshift down    </td><td>PGDOWN</td></tr>
    <tr><td>Switch shift modes</td><td>Q        </td></tr>
    <tr><td>Manual clutch     </td><td>SHIFT    </td></tr>
    <tr><td>Shift up          </td><td>A        </td></tr>
    <tr><td>Shift down        </td><td>Z        </td></tr>
</table>

### Misc

<table style="display: inline-block; vertical-align: top;">
    <tr bgcolor="#E5A36C"><th style="color: #000000">Misc</th><th>Key</th></tr>
    <tr><td>Truck horn        </td><td>H     </td></tr>
    <tr><td>Parking brake     </td><td>P     </td></tr>
    <tr><td>Trailer parking brake</td><td>CTRL+P</td></tr>
    <tr><td>Blinker left      </td><td>COMMA </td></tr>
    <tr><td>Blinker right     </td><td>DOT   </td></tr>
    <tr><td>Blinker warn      </td><td>PERIOD</td></tr>
    <tr><td>Toggle contact    </td><td>X     </td></tr>
    <tr><td>Starter (hold)    </td><td>S     </td></tr>
    <tr><td>Attach trailer    </td><td>L     </td></tr>
    <tr><td>Inter-wheel differentals</td><td>W</td></tr>
    <tr><td>Inter-axle differentals</td><td>CTRL+W</td></tr>
    <tr><td>Transfer case (2WD/4WD)</td><td>SHIFT+W</td></tr>
    <tr><td>Alternate gear ratios</td><td>ALT+W</td></tr>
    <tr><td>Secure Load       </td><td>O     </td></tr>
    <tr><td>Show skeleton     </td><td>K     </td></tr>
    <tr><td>Cycle skeleton views </td><td>CTRL+K</td></tr>
    <tr><td>Toggle lights     </td><td>N     </td></tr>
    <tr><td>Toggle beacons    </td><td>M     </td></tr>
    <tr><td>Rescue truck      </td><td>R     </td></tr>
    <tr><td>Particle cannon   </td><td>G     </td></tr>
</table>

### Commands

<table style="display: inline-block; vertical-align: top;">
    <tr bgcolor="#EC3F41"><th style="color: #000000">Function keys</th><th>Combo</th></tr>
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
    <tr><td>COMMANDS 48</td><td>CTRL + ALT + F12</td></tr>
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

## Aerial and marine controls

<img src="/images/input-map-aerial-and-marine.png" alt="Planes and boats keyboard layout" width="600"/>

### Planes

<table style="display: inline-block; vertical-align: top;">
    <tr bgcolor="#5FAC5E"><th style="color: #000000">Airplane controls</th><th>Key</th></tr>
    <tr><td>Steer left   </td><td>LEFT              </td></tr>
    <tr><td>Steer right  </td><td>RIGHT             </td></tr>
    <tr><td>Elevator up  </td><td>UP                </td></tr>
    <tr><td>Elevator down</td><td>DOWN              </td></tr>
    <tr><td>Rudder right </td><td>X                 </td></tr>
    <tr><td>Rudder left  </td><td>Z                 </td></tr>
    <tr><td>Brake        </td><td>B                 </td></tr>
    <tr><td>Parking brake</td><td>P                 </td></tr>
    <tr><td>Reverse      </td><td>R                 </td></tr>
    <tr><td>Less flaps   </td><td>1                 </td></tr>
    <tr><td>More flaps   </td><td>2                 </td></tr>
    <tr><td>Less airbrakes*</td><td>3               </td></tr>
    <tr><td>More airbrakes*</td><td>4               </td></tr>
    <tr><td>Throttle down</td><td>PAGE-DOWN         </td></tr>
    <tr><td>Throttle up  </td><td>PAGE-UP           </td></tr>
    <tr><td>Start engines</td><td>CLICK BUTTONS "ON"</td></tr>
</table>

`*` Depending on the plane setup

It is recommended to use: `CTRL+Home` to start all engine of a plane and `CTRL+PAGE-UP` to full throttle all engines
because some planes could have more than 4 engines and you couldn't control them with your mouse.

### Boats

<table style="display: inline-block; vertical-align: top;">
    <tr bgcolor="#E5A36C"><th style="color: #000000">Boat controls</th><th>Key</th></tr>

    <tr><td>Throttle down  </td><td>DOWN   </td></tr>
    <tr><td>Throttle up    </td><td>UP    </td></tr>
    <tr><td>Steer left     </td><td>LEFT </td></tr>
    <tr><td>Steer right    </td><td>RIGHT</td></tr>
    <tr><td>Center rudder  </td><td>PGUP  </td></tr>
    <tr><td>Center throttle</td><td>PGDOWN   </td></tr>
</table>

# Config file 'input.map'

For all keys, see the [input.map](https://github.com/RigsOfRods/rigs-of-rods/blob/master/resources/skeleton/config/input.map) file on GitHub.


This file defines all key alias for RoR. It has the following format:

    EVENT_NAME    EVENT_TYPE    MAPPING

For example:

    BOAT_CENTER_RUDDER     Keyboard    DOWN

This binds the <b>BOAT\_CENTER\_RUDDER</b> event to the <b>Down</b> arrow on your keyboard.

A list of all valid events can be found in the [Keypress Events](#keypress-events) section.

## Keyboard

For the keyboard there are several special things:

### Modifiers
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

In this example, COMMANDS_01 would be triggered if you press CTRL+F1, as F1 is part of the COMMANDS_13 combination.

    COMMANDS_01                    Keyboard             F1 
    COMMANDS_13                    Keyboard             CTRL+F1 

### List of usable keys

```
0
1
2
3
4
5
6
7
8
9
A
ABNT_C1
ABNT_C2
ADD
APOSTROPHE
APPS
AT
AX
B
BACK
BACKSLASH
C
CALCULATOR
CAPITAL
COLON
COMMA
CONVERT
D
DECIMAL
DELETE
DIVIDE
DOWN
E
END
EQUALS
ESCAPE
F
F1
F10
F11
F12
F13
F14
F15
F2
F3
F4
F5
F6
F7
F8
F9
G
GRAVE
H
HOME
I
INSERT
J
K
KANA
KANJI
L
LBRACKET
LCONTROL
LEFT
LMENU
LSHIFT
LWIN
M
MAIL
MEDIASELECT
MEDIASTOP
MINUS
MULTIPLY
MUTE
MYCOMPUTER
N
NEXTTRACK
NOCONVERT
NUMLOCK
NUMPAD0
NUMPAD1
NUMPAD2
NUMPAD3
NUMPAD4
NUMPAD5
NUMPAD6
NUMPAD7
NUMPAD8
NUMPAD9
NUMPADCOMMA
NUMPADENTER
NUMPADEQUALS
O
OEM_102
P
PAUSE
PERIOD
PGDOWN
PGUP
PLAYPAUSE
POWER
PREVTRACK
Q
R
RBRACKET
RCONTROL
RETURN
RIGHT
RMENU
RSHIFT
RWIN
S
SCROLL
SEMICOLON
SLASH
SLEEP
SPACE
STOP
SUBTRACT
SYSRQ
T
TAB
U
UNDERLINE
UNLABELED
UP
V
VOLUMEDOWN
VOLUMEUP
W
WAKE
WEBBACK
WEBFAVORITES
WEBFORWARD
WEBHOME
WEBREFRESH
WEBSEARCH
WEBSTOP
X
Y
YEN
Z
```


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

# Keypress Events

**Keypress event identification in RoR 0.4.7.0+**

These are all the valid keypress events, they can be used in a input map or for [prop animations](http://docs.rigsofrods.org/vehicle-creation/fileformat-truck/#add_animation). not all make sense though for animated props.

```
AIRPLANE_AIRBRAKES_FULL     
AIRPLANE_AIRBRAKES_LESS     
AIRPLANE_AIRBRAKES_MORE     
AIRPLANE_AIRBRAKES_NONE     
AIRPLANE_BRAKE              
AIRPLANE_ELEVATOR_DOWN      
AIRPLANE_ELEVATOR_UP        
AIRPLANE_FLAPS_FULL         
AIRPLANE_FLAPS_LESS         
AIRPLANE_FLAPS_MORE         
AIRPLANE_FLAPS_NONE         
AIRPLANE_PARKING_BRAKE      
AIRPLANE_REVERSE            
AIRPLANE_RUDDER_LEFT        
AIRPLANE_RUDDER_RIGHT       
AIRPLANE_STEER_LEFT         
AIRPLANE_STEER_RIGHT        
AIRPLANE_THROTTLE_AXIS      
AIRPLANE_THROTTLE_DOWN      
AIRPLANE_THROTTLE_FULL      
AIRPLANE_THROTTLE_NO        
AIRPLANE_THROTTLE_UP        
AIRPLANE_TOGGLE_ENGINES     
BOAT_CENTER_RUDDER          
BOAT_REVERSE                
BOAT_STEER_LEFT             
BOAT_STEER_RIGHT            
BOAT_THROTTLE_AXIS          
BOAT_THROTTLE_UP            
BOAT_THROTTLE_DOWN          
CAMERA_CHANGE               
CAMERA_FREE_MODE            
CAMERA_FREE_MODE_FIX        
CAMERA_LOOKBACK             
CAMERA_RESET                
CAMERA_UP                   
CAMERA_DOWN                 
CAMERA_ROTATE_DOWN          
CAMERA_ROTATE_LEFT          
CAMERA_ROTATE_RIGHT         
CAMERA_ROTATE_UP            
CAMERA_ZOOM_IN              
CAMERA_ZOOM_IN_FAST         
CAMERA_ZOOM_OUT             
CAMERA_ZOOM_OUT_FAST        
SKY_DECREASE_TIME           
SKY_DECREASE_TIME_FAST      
SKY_INCREASE_TIME           
SKY_INCREASE_TIME_FAST      
CHARACTER_BACKWARDS         
CHARACTER_FORWARD           
CHARACTER_JUMP              
CHARACTER_LEFT              
CHARACTER_RIGHT             
CHARACTER_ROT_DOWN          
CHARACTER_ROT_UP            
CHARACTER_RUN               
CHARACTER_RUN               
CHARACTER_SIDESTEP_LEFT     
CHARACTER_SIDESTEP_RIGHT    
COMMANDS_01                 
COMMANDS_02                 
COMMANDS_03                 
COMMANDS_04                 
COMMANDS_05                 
COMMANDS_06                 
COMMANDS_07                 
COMMANDS_08                 
COMMANDS_09                 
COMMANDS_10                 
COMMANDS_11                 
COMMANDS_12                 
COMMANDS_13                 
COMMANDS_14                 
COMMANDS_15                 
COMMANDS_16                 
COMMANDS_17                 
COMMANDS_18                 
COMMANDS_19                 
COMMANDS_20                 
COMMANDS_21                 
COMMANDS_22                 
COMMANDS_23                 
COMMANDS_24                 
COMMANDS_25                 
COMMANDS_26                 
COMMANDS_27                 
COMMANDS_28                 
COMMANDS_29                 
COMMANDS_30                 
COMMANDS_31                 
COMMANDS_32                 
COMMANDS_33                 
COMMANDS_34                 
COMMANDS_35                 
COMMANDS_36                 
COMMANDS_37                 
COMMANDS_38                 
COMMANDS_39                 
COMMANDS_40                 
COMMANDS_41                 
COMMANDS_42                 
COMMANDS_43                 
COMMANDS_44                 
COMMANDS_45                 
COMMANDS_46                 
COMMANDS_47                 
COMMANDS_48                 
COMMANDS_49                 
COMMANDS_50                 
COMMANDS_51                 
COMMANDS_52                 
COMMANDS_53                 
COMMANDS_54                 
COMMANDS_55                 
COMMANDS_56                 
COMMANDS_57                 
COMMANDS_58                 
COMMANDS_59                 
COMMANDS_60                 
COMMANDS_61                 
COMMANDS_62                 
COMMANDS_63                 
COMMANDS_64                 
COMMANDS_65                 
COMMANDS_66                 
COMMANDS_67                 
COMMANDS_68                 
COMMANDS_69                 
COMMANDS_70                 
COMMANDS_71                 
COMMANDS_72                 
COMMANDS_73                 
COMMANDS_74                 
COMMANDS_75                 
COMMANDS_76                 
COMMANDS_77                 
COMMANDS_78                 
COMMANDS_79                 
COMMANDS_80                 
COMMANDS_81                 
COMMANDS_82                 
COMMANDS_83                 
COMMANDS_84                 
COMMON_ACCELERATE_SIMULATION
COMMON_DECELERATE_SIMULATION
COMMON_RESET_SIMULATION_PACE
COMMON_CONSOLE_TOGGLE       
COMMON_ENTER_OR_EXIT_TRUCK  
COMMON_ENTER_NEXT_TRUCK     
COMMON_ENTER_PREVIOUS_TRUCK 
COMMON_REMOVE_CURRENT_TRUCK 
COMMON_RESPAWN_LAST_TRUCK   
COMMON_FULLSCREEN_TOGGLE    
COMMON_HIDE_GUI             
COMMON_LOCK                 
COMMON_AUTOLOCK             
COMMON_ROPELOCK             
COMMON_OUTPUT_POSITION      
COMMON_GET_NEW_VEHICLE      
COMMON_PRESSURE_LESS        
COMMON_PRESSURE_MORE        
COMMON_QUIT_GAME            
COMMON_REPLAY_BACKWARD      
COMMON_REPLAY_FAST_BACKWARD 
COMMON_REPLAY_FAST_FORWARD  
COMMON_REPLAY_FORWARD       
COMMON_RESCUE_TRUCK         
COMMON_RESET_TRUCK          
COMMON_SCREENSHOT           
COMMON_SECURE_LOAD          
COMMON_SHOW_SKELETON        
COMMON_TOGGLE_TERRAIN_EDITOR
COMMON_TOGGLE_CUSTOM_PARTICL
COMMON_TOGGLE_MAT_DEBUG     
COMMON_TOGGLE_RENDER_MODE   
COMMON_TOGGLE_REPLAY_MODE   
COMMON_TOGGLE_STATS         
COMMON_TOGGLE_TRUCK_BEACONS 
COMMON_TOGGLE_TRUCK_LIGHTS  
COMMON_TRUCK_INFO           
COMMON_TRUCK_DESCRIPTION    
COMMON_FOV_LESS             
COMMON_FOV_MORE             
GRASS_LESS                  
GRASS_MORE                  
GRASS_MOST                  
GRASS_NONE                  
GRASS_SAVE                  
SURVEY_MAP_ZOOM_IN          
SURVEY_MAP_ZOOM_OUT         
SURVEY_MAP_TOGGLE_VIEW      
SURVEY_MAP_TOGGLE_ALPHA     
SURVEY_MAP_TOGGLE_ICONS     
MENU_DOWN                   
MENU_LEFT                   
MENU_RIGHT                  
MENU_SELECT                 
MENU_UP                     
TRUCK_ACCELERATE            
TRUCK_ACCELERATE_MODIFIER_25
TRUCK_ACCELERATE_MODIFIER_50
TRUCK_ANTILOCK_BRAKE        
TRUCK_AUTOSHIFT_DOWN        
TRUCK_AUTOSHIFT_UP          
TRUCK_BLINK_LEFT            
TRUCK_BLINK_RIGHT           
TRUCK_BLINK_WARN            
TRUCK_BRAKE                 
TRUCK_BRAKE_MODIFIER_25     
TRUCK_BRAKE_MODIFIER_50     
TRUCK_CRUISE_CONTROL        
TRUCK_CRUISE_CONTROL_READJUS
TRUCK_CRUISE_CONTROL_ACCL   
TRUCK_CRUISE_CONTROL_DECL   
TRUCK_HORN                  
TRUCK_LIGHTTOGGLE1          
TRUCK_LIGHTTOGGLE2          
TRUCK_LIGHTTOGGLE3          
TRUCK_LIGHTTOGGLE4          
TRUCK_LIGHTTOGGLE5          
TRUCK_LIGHTTOGGLE6          
TRUCK_LIGHTTOGGLE7          
TRUCK_LIGHTTOGGLE8          
TRUCK_LIGHTTOGGLE9          
TRUCK_LIGHTTOGGLE10         
TRUCK_MANUAL_CLUTCH         
TRUCK_PARKING_BRAKE         
TRUCK_SHIFT_DOWN            
TRUCK_SHIFT_NEUTRAL         
TRUCK_SHIFT_UP              
TRUCK_STARTER               
TRUCK_STEER_LEFT            
TRUCK_STEER_RIGHT           
TRUCK_SWITCH_SHIFT_MODES    
TRUCK_TOGGLE_AXLE_LOCK      
TRUCK_TOGGLE_CONTACT        
TRUCK_TOGGLE_FORWARDCOMMANDS
TRUCK_TOGGLE_IMPORTCOMMANDS 
TRUCK_TOGGLE_VIDEOCAMERA    
TRUCK_TRACTION_CONTROL      
```

# Mouse


### Required applications

[vJoy joystick emulator](http://vjoystick.sourceforge.net/site/index.php/download-a-install/72-download)

[FreePIE input emulator](http://andersmalmgren.github.io/FreePIE/index.html)

### Setting up the input map and FreePIE script

After installing the above applications, download [this zip file](/download/RoR_Mouse_Control.zip) which contains the required input map and FreePIE script.

There will be two files in the zip: `vJoy_Device.map` and `MouseControl.py`. 

Extract both files into `Documents\Rigs of Rods 0.4\config`.

### Using FreePIE

Open FreePIE and press `File -> Open`. Browse to the `MouseControl.py` file you downloaded earlier:

![1](/images/FreePIE-1.png)

![2](/images/FreePIE-2.png)

![3](/images/FreePIE-3.png)

Then press `Script -> Run script`:

![4](/images/FreePIE-4.png)

The script should now be running. If you get an error, install vJoy.

Leave FreePIE running, launch RoR and you should now have mouse control!

You can modify both the script and the input map to make them better suit for your use. 

For example the numbers `40` and `80` in the script are the sensitivity of the controls.

Mouse middle button in the script above, will reset the axises in game, in this case the steering and throttle.

# Configuring controls with the Input Mapping Tool

The easiest way to configure your device for use in Rigs of Rods is to use the [Input Mapping Tool](https://forum.rigsofrods.org/resources/windows-input-mapping-tool.13/).

## vJoy Conflicts

**NOTE: If you have vJoy installed, you will have to disable it before running the tool!**

![vJoyDisable](/images/vJoyDisable.png)

## Launching the tool

After downloading, extract the zip into a new folder. Then double-click `Run.bat` to launch the tool. 

![5](/images/InputMappingTool-1.png)

## Adding new inputs

To begin adding inputs, click `Add`.

![6](/images/InputMappingTool-2.png)

Select the event you want to assign an input to. In this exanmple, I will use `TRUCK_ACCELERATE`

Then select the correct input type:

<table style="color: #111111; display: inline-block; vertical-align: top;">
<tr><td>Event type</td><td>Description</td></tr>
<tr><td>Keyboard</td><td>All keys on the keyboard.</td></tr>
<tr><td>JoystickAxis</td><td>Used for steering wheels/sticks/etc.</td></tr>
<tr><td>JoystickSlider</td><td>Any type of slider, mainly seen on flight sticks.</td></tr>
<tr><td>JoystickButton</td><td>Buttons! (e.g. `A` button on an Xbox controller)</td></tr>
<tr><td>JoystickPov</td><td>Used for D-Pad controls.</td></tr>
</table>

Click `Add` once ready, the tool will then ask you to move the axis/press a button. 

The popup will automatically close once the requested action is completed.

![7](/images/InputMappingTool-3.png)

Repeat the process for all the inputs you want to add.

![8](/images/InputMappingTool-4.png)

Once you're done, it's time to export the keymap.

## Exporting the keymap

First, you'll need to get the correct file name of your file.

To do this, double-click `getdeviceinfo.exe`. This will generate a `inputinfo.txt` file. Open the text file.

Example output:

```
System info:
	OIS Version: 1.3.0
	OIS Release Name: 1.3.0
	Input Manager: Win32InputManager
	Total Keyboards: 1
	Total Mice: 1
	Total JoySticks: 1

Devices:
	- OISKeyboard, Vendor: Win32InputManager
	- OISMouse, Vendor: Win32InputManager
	- OISJoyStick, Vendor: Logitech Extreme 3D


Joystick 0:
	Vendor: Logitech Extreme 3D
	VendorMapFilename: Logitech_Extreme_3D.map
	ID: 0
	Type: [3] OISJoyStick
	Axes: 3
	Sliders: 1
	POV/HATs: 1
	Buttons: 12
	Vector3: 0
	Vector3Sensitivity: 2.28
```

`VendorMapFilename` will be the name of your exported file. In this example, the name will be `Logitech_Extreme_3D.map`.

Click `Export Keymap` then select your device from the list.

![9](/images/InputMappingTool-5.png)

![10](/images/InputMappingTool-6.png)

And finally, run Rigs of Rods and test your device! You can make further edits to your input map by clicking `Import Keymap`.

If you want to share your created input map, upload it to the Miscellaneous section of the [Repository](https://forum.rigsofrods.org/resources/). Thanks!
