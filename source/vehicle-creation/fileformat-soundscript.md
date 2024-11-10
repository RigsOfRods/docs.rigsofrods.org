Soundscript file reference
============



This format is text-based and files must have the extension ".soundscript". 

Each soundscript file can contain the description of many sound scripts. 
Each sound script defines how to play one or many audio files 
in the context of the vehicle where it is used (using the [soundsources section](fileformat-truck.md)). 

A sound script is defined by a line with his name 
(which is the name you use in the soundsource section of your vehicle description file),
 then a set of curly braces enclosing parameters.
 
 <br><!-- Hack to make space for `trigger_source` table -->
 <br>
 <br>
 <br> 

## Parameters

### Sources

Sources define which vehicle events or states will influence the sound. 

#### trigger_source

This is the more important source, and it is mandatory. There can be only one trigger source. It will define how the sound will start and stop. Valid values are: 


| Source                       | Description
| ---                          | ---
| always_on                    | The sound will always play 
| engine                       | The sound will play as long as the car/truck/boat engine is running 
| aeroengine1<br>to aeroengine8   | The sound will play as long as the numbered propeller or jet engine is running 
| afterburner1<br>to afterburner8 | Same for afterburners 
| horn                         | The horn 
| brake                        | The brake pedal 
| pump                         | The hydraulic pump 
| starter                      | The engine starter 
| turbo_BOV				| Turbo blow off valve
| turbo_waste_gate				| Turbo waste gate 
| turbo_back_fire				| Turbo back fire 
| ignition                     | The ignition switch 
| repair                       | When the truck is repaired 
| air                          | Active air suspension activation 
| air_purge                    | Compressed air purge 
| shift                        | Shifting gears 
| gear_slide                   | Gearbox torture 
| reverse_gear                  | In reverse gear 
| turn_signal                  | Turn signal toggle 
| turn_signal_tick                  | Turn signal ticking 
| turn_signal_warn_tick                  | Emergency signals
| antilock                   | Anti-lock brakes toggle 
| tractioncontrol                   | Traction control toggle
| creak                        | Structural creaking 
| break                        | Beam breaking 
| screetch                     | Wheel screetching on tarmac 
| parking_brake                | Parking brake 
| aoa_horn                     | Stall horn (AOA above 18 degree) 
| avionic_chat_01<br>to avionic_chat_13 | Airplane chatter
| gpws_ap_disconnect           | Autopilot disconnect 
| gpws_10                      | 10 feet warning 
| gpws_20                      | 20 feet warning 
| gpws_30                      | 30 feet warning 
| gpws_40                      | 40 feet warning 
| gpws_50                      | 50 feet warning 
| gpws_100                     | 100 feet warning 
| gpws_pull_up                 | Woop woop pull up! 
| gpws_minimums                | Minimums!
| linked_command                | Command sounds
| main_menu                | Main menu music


#### pitch_source

A pitch source will alter the pitch of the played sounds (if they are pitchable). There can be only one pitch source. Valid pitch sources are: 


| Name                                            | Description
| ---                                             | ---
| none                                            | This is the default, no pitch modulation, with a reference value of 1.0 
| engine_rpm                                      | Engine revolutions per minute 
| turbo_rpm                                       | Turbo revolutions per minute 
| aeroengine1_rpm<br>to aeroengine8_rpm           | Propeller revolutions per minute, or jet engine speed in percent 
| aeroengine1_throttle<br>to aeroengine8_throttle | Throttle setting of the propeller or jet engine 
| wheel_speed_kmph                                | Wheel speed in kilometer per hour 
| air_speed_knots                                 | Air speed in knots 
| angle_of_attack_degree                          | Absolute value of the angle of attack in degree (for airplanes only) 
| injector_ratio                                  | How much fuel is injected into the engine (from 0.0 to 1.0) 
| torque_nm                                       | Output torque of engine in Newton.Meter 
| gearbox_rpm                                     | Gearbox output speed in RPM 
| creak                                           | Structural creaking effort 
| break                                           | Beam breaking effort 
| screetch                                        | Wheel screetch intensity 
| pump_rpm                                     | Hydraulic pump RPM
| linked_command_rate                  | Command movement rate 
| music_volume                           | Main menu music volume


#### gain_source

A gain source will alter the gain of the played sounds (how loud it is heard). 
There can be only one gain source. Valid gain sources are the same as for pitch sources. 

### Modifiers

Modifiers will take output value from the pitch or gain sources, 
and apply to it a polynomial equation (up to degree 2) to alter the value to match the intended effect. 
Both modifiers take two or three parameter values (they can be negative value): 

* An offset (default 0.0) 
* A multiplicative factor (default 1.0) 
* An optional square factor (default 0.0)

The equation is&nbsp;: output = offset + mult_factor x source + square_factor x source x source 

#### pitch_factors

The parameter pitch_factors alters the pitch source. It is optional. 

#### gain_factors 

The parameter gain_factors alters the gain source. It is optional. 
The output value of the gain modifier is clamped to the interval from 0.0 to 1.0 before being applied to the sounds. 

### Sounds

These parameters define the WAV sound files used by the soundscript. All sounds parameters takes two parameters&nbsp;: 

* a reference pitch value&nbsp;: this is the "true" pitch value corresponding to the recorded sound. For example, if you record an engine at 100 RPM, the resulting sound will have a reference pitch value of 100, and will be correctly pitched by the source engine RPM (as long as the units match, if not, use the modifiers). You can also use the keyword "unpitched" to say that this sound shall never be pitched. 
* a WAV file name. This WAV file **MUST** be mono, and exported as 16-bit PCM with no metadata.

#### start_sound 

This sound is optional and is played only once at the start of the trigger. There can be only one start sound. 

#### sound

This sound is optional and played in a loop as long as the trigger holds. There can be many sounds defined. If there are many sounds with different reference pitches, the sounds will be mixed together to obtain the best blend of sounds for a given source pitch. This allows the "texture" of sound to change depending on pitch. 

#### stop sound

This sound is optional and is played only once at the end of the trigger. There can be only one end sound. 

## Examples

Note that you can compose sound scripts by playing several scripts at the same time (with the same trigger). 
In the following, the full diesel engine sound is composed of the 3 first sound scripts played together. 

```
tracks/default_diesel
{
 trigger_source engine
 pitch_source engine_rpm
 sound 750.0 default_diesel_idle.wav
 sound 849.0 default_diesel_low.wav
 sound 1035.0 default_diesel_medium.wav
 sound 1455.0 default_diesel_high.wav
}

tracks/default_force
{
 trigger_source engine
 gain_source injector_ratio
 gain_factors 0.0 0.5
 sound unpitched default_diesel_force.wav
}

tracks/default_turbo
{
 trigger_source engine
 pitch_source turbo_rpm
 gain_source turbo_rpm
 gain_factors 0.0 0.0 1.852E-12
 sound 100000.0 default_turbo.wav
}

tracks/default_starter
{
 trigger_source starter
 start_sound unpitched default_starter_start.wav
 sound unpitched default_starter.wav
 stop_sound unpitched default_starter_stop.wav
}

tracks/default_pump
{
 trigger_source pump
 pitch_source pump_rpm
 start_sound 660.0 default_pump_start.wav
 sound 660.0 default_pump.wav
 stop_sound 660.0 default_pump_stop.wav
}

tracks/default_brakes
{
 trigger_source brake
 stop_sound unpitched default_brakes.wav
}

tracks/default_parkbrakes
{
 trigger_source parking_brake
 start_sound unpitched default_parking_brakes.wav
}

```

## Default

These are the default soundscripts for RoR.&nbsp; It is divided into sections according to engine type.

### Engine (Diesel) 

```
tracks/default_diesel
{
 trigger_source engine
 pitch_source engine_rpm
 sound 750.0 default_diesel_idle.wav
 sound 849.0 default_diesel_low.wav
 sound 1035.0 default_diesel_medium.wav
 sound 1455.0 default_diesel_high.wav
}

tracks/default_force
{
 trigger_source engine
 gain_source injector_ratio
 gain_factors 0.0 0.5
 sound unpitched default_diesel_force.wav
}

tracks/default_starter
{
 trigger_source starter
 start_sound unpitched default_starter_start.wav
 sound unpitched default_starter.wav
 stop_sound unpitched default_starter_stop.wav
}

tracks/default_turbo
{
 trigger_source engine
 pitch_source turbo_rpm
 gain_source turbo_rpm
 gain_factors 0.0 0.0 1.852E-12
 sound 100000.0 default_turbo.wav
}

tracks/default_air_purge
{
 trigger_source air_purge
 sound unpitched default_valve.wav
}

tracks/default_horn
{
 trigger_source horn
 start_sound unpitched default_horn_start.wav
 sound unpitched default_horn.wav
 stop_sound unpitched default_horn_stop.wav
}

tracks/default_pump
{
 trigger_source pump
 pitch_source pump_rpm
 start_sound 660.0 default_pump_start.wav
 sound 660.0 default_pump.wav
 stop_sound 660.0 default_pump_stop.wav
}

tracks/default_screetch
{
 trigger_source screetch
 gain_source screetch
 sound unpitched default_screetch.wav
}

tracks/default_brakes
{
 trigger_source brake
 stop_sound unpitched default_brakes.wav
}

tracks/default_parkbrakes
{
 trigger_source parking_brake
 start_sound unpitched default_parking_brakes.wav
}

tracks/default_air
{
 trigger_source air
 sound unpitched default_air.wav
}

tracks/default_shift
{
 trigger_source shift
 start_sound unpitched default_shift.wav
}

tracks/default_break
{
 trigger_source break
 pitch_source break
 pitch_factors 1.0 1.0
 start_sound 1.0 default_break.wav
}

tracks/default_creak
{
 trigger_source creak
 pitch_source creak
 pitch_factors 1.0 0.2
 gain_source creak
 gain_factors 0.3 1.0
 start_sound 1.0 default_creak.wav
}

tracks/default_gear_slide
{
 trigger_source gear_slide
 start_sound unpitched default_gear_slide.wav
}

tracks/default_reverse_beep
{
 trigger_source reverse_gear
 sound unpitched default_reverse_beep.wav
}

tracks/default_turn_signal
{
 trigger_source turn_signal
 sound unpitched default_turn_signal.wav
}
``` 

### Engine (Gasoline) 

```
tracks/default_car
{
 trigger_source engine
 pitch_source engine_rpm
 gain_source injector_ratio
 gain_factors 0.5 0.5
 sound 1500 default_car_idle.wav
}

tracks/default_starter
{
 trigger_source starter
 start_sound unpitched default_starter_start.wav
 sound unpitched default_starter.wav
 stop_sound unpitched default_starter_stop.wav
}

tracks/default_horn
{
 trigger_source horn
 start_sound unpitched default_horn_start.wav
 sound unpitched default_horn.wav
 stop_sound unpitched default_horn_stop.wav
}

tracks/default_pump
{
 trigger_source pump
 pitch_source pump_rpm
 start_sound 660.0 default_pump_start.wav
 sound 660.0 default_pump.wav
 stop_sound 660.0 default_pump_stop.wav
}

tracks/default_police
{
 trigger_source horn
 sound unpitched default_police.wav
}

tracks/default_screetch
{
 trigger_source screetch
 gain_source screetch
 sound unpitched default_screetch.wav
}

tracks/default_shift
{
 trigger_source shift
 start_sound unpitched default_shift.wav
}

tracks/default_break
{
 trigger_source break
 pitch_source break
 pitch_factors 1.0 1.0
 start_sound 1.0 default_break.wav
}

tracks/default_creak
{
 trigger_source creak
 pitch_source creak
 pitch_factors 1.0 0.2
 gain_source creak
 gain_factors 0.3 1.0
 start_sound 1.0 default_creak.wav
}

tracks/default_gear_slide
{
 trigger_source gear_slide
 start_sound unpitched default_gear_slide.wav
}

tracks/default_turn_signal
{
 trigger_source turn_signal
 sound unpitched default_turn_signal.wav
}
``` 

### Airplane (Prop) 

```
tracks/default_turboprop_start1
{
 trigger_source aeroengine1
 start_sound unpitched default_turboprop_start.wav
}

tracks/default_turboprop_lopower1
{
 trigger_source always_on
 pitch_source aeroengine1_rpm
 gain_source aeroengine1_throttle
 gain_factors 0.5 0.5
 sound 1000.0 default_turboprop_lopower.wav
}

tracks/default_turboprop_hipower1
{
 trigger_source aeroengine1
 pitch_source aeroengine1_rpm
 gain_source aeroengine1_throttle
 gain_factors -0.5 1.0
 sound 1000.0 default_turboprop_hipower.wav
}

tracks/default_turboprop_start2
{
 trigger_source aeroengine2
 start_sound unpitched default_turboprop_start.wav
}

tracks/default_turboprop_lopower2
{
 trigger_source always_on
 pitch_source aeroengine2_rpm
 gain_source aeroengine2_throttle
 gain_factors 0.5 0.5
 sound 1000.0 default_turboprop_lopower.wav
}

tracks/default_turboprop_hipower2
{
 trigger_source aeroengine2
 pitch_source aeroengine2_rpm
 gain_source aeroengine2_throttle
 gain_factors -0.5 1.0
 sound 1000.0 default_turboprop_hipower.wav
}

tracks/default_turboprop_start3
{
 trigger_source aeroengine3
 start_sound unpitched default_turboprop_start.wav
}

tracks/default_turboprop_lopower3
{
 trigger_source always_on
 pitch_source aeroengine3_rpm
 gain_source aeroengine3_throttle
 gain_factors 0.5 0.5
 sound 1000.0 default_turboprop_lopower.wav
}

tracks/default_turboprop_hipower3
{
 trigger_source aeroengine3
 pitch_source aeroengine3_rpm
 gain_source aeroengine3_throttle
 gain_factors -0.5 1.0
 sound 1000.0 default_turboprop_hipower.wav
}

tracks/default_turboprop_start4
{
 trigger_source aeroengine4
 start_sound unpitched default_turboprop_start.wav
}

tracks/default_turboprop_lopower4
{
 trigger_source always_on
 pitch_source aeroengine4_rpm
 gain_source aeroengine4_throttle
 gain_factors 0.5 0.5
 sound 1000.0 default_turboprop_lopower.wav
}

tracks/default_turboprop_hipower4
{
 trigger_source aeroengine4
 pitch_source aeroengine4_rpm
 gain_source aeroengine4_throttle
 gain_factors -0.5 1.0
 sound 1000.0 default_turboprop_hipower.wav
}

tracks/default_turboprop_start5
{
 trigger_source aeroengine5
 start_sound unpitched default_turboprop_start.wav
}

tracks/default_turboprop_lopower5
{
 trigger_source always_on
 pitch_source aeroengine5_rpm
 gain_source aeroengine5_throttle
 gain_factors 0.5 0.5
 sound 1000.0 default_turboprop_lopower.wav
}

tracks/default_turboprop_hipower5
{
 trigger_source aeroengine5
 pitch_source aeroengine5_rpm
 gain_source aeroengine5_throttle
 gain_factors -0.5 1.0
 sound 1000.0 default_turboprop_hipower.wav
}

tracks/default_turboprop_start6
{
 trigger_source aeroengine6
 start_sound unpitched default_turboprop_start.wav
}

tracks/default_turboprop_lopower6
{
 trigger_source always_on
 pitch_source aeroengine6_rpm
 gain_source aeroengine6_throttle
 gain_factors 0.5 0.5
 sound 1000.0 default_turboprop_lopower.wav
}

tracks/default_turboprop_hipower6
{
 trigger_source aeroengine6
 pitch_source aeroengine6_rpm
 gain_source aeroengine6_throttle
 gain_factors -0.5 1.0
 sound 1000.0 default_turboprop_hipower.wav
}

tracks/default_turboprop_start7
{
 trigger_source aeroengine7
 start_sound unpitched default_turboprop_start.wav
}

tracks/default_turboprop_lopower7
{
 trigger_source always_on
 pitch_source aeroengine7_rpm
 gain_source aeroengine7_throttle
 gain_factors 0.5 0.5
 sound 1000.0 default_turboprop_lopower.wav
}

tracks/default_turboprop_hipower7
{
 trigger_source aeroengine7
 pitch_source aeroengine7_rpm
 gain_source aeroengine7_throttle
 gain_factors -0.5 1.0
 sound 1000.0 default_turboprop_hipower.wav
}

tracks/default_turboprop_start8
{
 trigger_source aeroengine8
 start_sound unpitched default_turboprop_start.wav
}

tracks/default_turboprop_lopower8
{
 trigger_source always_on
 pitch_source aeroengine8_rpm
 gain_source aeroengine8_throttle
 gain_factors 0.5 0.5
 sound 1000.0 default_turboprop_lopower.wav
}

tracks/default_turboprop_hipower8
{
 trigger_source aeroengine8
 pitch_source aeroengine8_rpm
 gain_source aeroengine8_throttle
 gain_factors -0.5 1.0
 sound 1000.0 default_turboprop_hipower.wav
}
``` 

### Airplane (Jet) 

```
tracks/default_turbojet_start1
{
 trigger_source aeroengine1
 start_sound unpitched default_turbojet_start.wav
}

tracks/default_turbojet_lopower1
{
 trigger_source always_on
 pitch_source aeroengine1_rpm
 gain_source aeroengine1_rpm
 gain_factors 2.0 -0.02
 sound 25.0 default_turbojet_lopower.wav
}

tracks/default_turbojet_hipower1
{
 trigger_source aeroengine1
 gain_source aeroengine1_rpm
 gain_factors -0.30 0.013
 sound unpitched default_turbojet_hipower.wav
}

tracks/default_turbojet_afterburner1
{
 trigger_source afterburner1
 sound unpitched default_turbojet_afterburner.wav
}

tracks/default_turbojet_start2
{
 trigger_source aeroengine2
 start_sound unpitched default_turbojet_start.wav
}

tracks/default_turbojet_lopower2
{
 trigger_source always_on
 pitch_source aeroengine2_rpm
 gain_source aeroengine2_rpm
 gain_factors 2.0 -0.02
 sound 25.0 default_turbojet_lopower.wav
}

tracks/default_turbojet_hipower2
{
 trigger_source aeroengine2
 gain_source aeroengine2_rpm
 gain_factors -0.30 0.013
 sound unpitched default_turbojet_hipower.wav
}

tracks/default_turbojet_afterburner2
{
 trigger_source afterburner2
 sound unpitched default_turbojet_afterburner.wav
}

tracks/default_turbojet_start3
{
 trigger_source aeroengine3
 start_sound unpitched default_turbojet_start.wav
}

tracks/default_turbojet_lopower3
{
 trigger_source always_on
 pitch_source aeroengine3_rpm
 gain_source aeroengine3_rpm
 gain_factors 2.0 -0.02
 sound 25.0 default_turbojet_lopower.wav
}

tracks/default_turbojet_hipower3
{
 trigger_source aeroengine3
 gain_source aeroengine3_rpm
 gain_factors -0.30 0.013
 sound unpitched default_turbojet_hipower.wav
}

tracks/default_turbojet_afterburner3
{
 trigger_source afterburner3
 sound unpitched default_turbojet_afterburner.wav
}

tracks/default_turbojet_start4
{
 trigger_source aeroengine4
 start_sound unpitched default_turbojet_start.wav
}

tracks/default_turbojet_lopower4
{
 trigger_source always_on
 pitch_source aeroengine4_rpm
 gain_source aeroengine4_rpm
 gain_factors 2.0 -0.02
 sound 25.0 default_turbojet_lopower.wav
}

tracks/default_turbojet_hipower4
{
 trigger_source aeroengine4
 gain_source aeroengine4_rpm
 gain_factors -0.30 0.013
 sound unpitched default_turbojet_hipower.wav
}

tracks/default_turbojet_afterburner4
{
 trigger_source afterburner4
 sound unpitched default_turbojet_afterburner.wav
}

tracks/default_turbojet_start5
{
 trigger_source aeroengine5
 start_sound unpitched default_turbojet_start.wav
}

tracks/default_turbojet_lopower5
{
 trigger_source always_on
 pitch_source aeroengine5_rpm
 gain_source aeroengine5_rpm
 gain_factors 2.0 -0.02
 sound 25.0 default_turbojet_lopower.wav
}

tracks/default_turbojet_hipower5
{
 trigger_source aeroengine5
 gain_source aeroengine5_rpm
 gain_factors -0.30 0.013
 sound unpitched default_turbojet_hipower.wav
}

tracks/default_turbojet_afterburner5
{
 trigger_source afterburner5
 sound unpitched default_turbojet_afterburner.wav
}

tracks/default_turbojet_start6
{
 trigger_source aeroengine6
 start_sound unpitched default_turbojet_start.wav
}

tracks/default_turbojet_lopower6
{
 trigger_source always_on
 pitch_source aeroengine6_rpm
 gain_source aeroengine6_rpm
 gain_factors 2.0 -0.02
 sound 25.0 default_turbojet_lopower.wav
}

tracks/default_turbojet_hipower6
{
 trigger_source aeroengine6
 gain_source aeroengine6_rpm
 gain_factors -0.30 0.013
 sound unpitched default_turbojet_hipower.wav
}

tracks/default_turbojet_afterburner6
{
 trigger_source afterburner6
 sound unpitched default_turbojet_afterburner.wav
}

tracks/default_turbojet_start7
{
 trigger_source aeroengine7
 start_sound unpitched default_turbojet_start.wav
}

tracks/default_turbojet_lopower7
{
 trigger_source always_on
 pitch_source aeroengine7_rpm
 gain_source aeroengine7_rpm
 gain_factors 2.0 -0.02
 sound 25.0 default_turbojet_lopower.wav
}

tracks/default_turbojet_hipower7
{
 trigger_source aeroengine7
 gain_source aeroengine7_rpm
 gain_factors -0.30 0.013
 sound unpitched default_turbojet_hipower.wav
}

tracks/default_turbojet_afterburner7
{
 trigger_source afterburner7
 sound unpitched default_turbojet_afterburner.wav
}

tracks/default_turbojet_start8
{
 trigger_source aeroengine8
 start_sound unpitched default_turbojet_start.wav
}

tracks/default_turbojet_lopower8
{
 trigger_source always_on
 pitch_source aeroengine8_rpm
 gain_source aeroengine8_rpm
 gain_factors 2.0 -0.02
 sound 25.0 default_turbojet_lopower.wav
}

tracks/default_turbojet_hipower8
{
 trigger_source aeroengine8
 gain_source aeroengine8_rpm
 gain_factors -0.30 0.013
 sound unpitched default_turbojet_hipower.wav
}

tracks/default_turbojet_afterburner8
{
 trigger_source afterburner8
 sound unpitched default_turbojet_afterburner.wav
}</pre> 

==== Airplane (Piston)  ====

<pre>tracks/default_pistonprop_start1
{
 trigger_source aeroengine1
 start_sound unpitched default_pistonprop_start.wav
}

tracks/default_pistonprop_lopower1
{
 trigger_source always_on
 pitch_source aeroengine1_rpm
 gain_source aeroengine1_throttle
 gain_factors 0.5 0.5
 sound 1000.0 default_pistonprop_lopower.wav
}

tracks/default_pistonprop_hipower1
{
 trigger_source aeroengine1
 pitch_source aeroengine1_rpm
 gain_source aeroengine1_throttle
 gain_factors -0.5 1.0
 sound 1000.0 default_pistonprop_hipower.wav
}

tracks/default_pistonprop_start2
{
 trigger_source aeroengine2
 start_sound unpitched default_pistonprop_start.wav
}

tracks/default_pistonprop_lopower2
{
 trigger_source always_on
 pitch_source aeroengine2_rpm
 gain_source aeroengine2_throttle
 gain_factors 0.5 0.5
 sound 1000.0 default_pistonprop_lopower.wav
}

tracks/default_pistonprop_hipower2
{
 trigger_source aeroengine2
 pitch_source aeroengine2_rpm
 gain_source aeroengine2_throttle
 gain_factors -0.5 1.0
 sound 1000.0 default_pistonprop_hipower.wav
}

tracks/default_pistonprop_start3
{
 trigger_source aeroengine3
 start_sound unpitched default_pistonprop_start.wav
}

tracks/default_pistonprop_lopower3
{
 trigger_source always_on
 pitch_source aeroengine3_rpm
 gain_source aeroengine3_throttle
 gain_factors 0.5 0.5
 sound 1000.0 default_pistonprop_lopower.wav
}

tracks/default_pistonprop_hipower3
{
 trigger_source aeroengine3
 pitch_source aeroengine3_rpm
 gain_source aeroengine3_throttle
 gain_factors -0.5 1.0
 sound 1000.0 default_pistonprop_hipower.wav
}

tracks/default_pistonprop_start4
{
 trigger_source aeroengine4
 start_sound unpitched default_pistonprop_start.wav
}

tracks/default_pistonprop_lopower4
{
 trigger_source always_on
 pitch_source aeroengine4_rpm
 gain_source aeroengine4_throttle
 gain_factors 0.5 0.5
 sound 1000.0 default_pistonprop_lopower.wav
}

tracks/default_pistonprop_hipower4
{
 trigger_source aeroengine4
 pitch_source aeroengine4_rpm
 gain_source aeroengine4_throttle
 gain_factors -0.5 1.0
 sound 1000.0 default_pistonprop_hipower.wav
}

tracks/default_pistonprop_lopower5
{
 trigger_source always_on
 pitch_source aeroengine5_rpm
 gain_source aeroengine5_throttle
 gain_factors 0.5 0.5
 sound 1000.0 default_pistonprop_lopower.wav
}

tracks/default_pistonprop_hipower5
{
 trigger_source aeroengine5
 pitch_source aeroengine5_rpm
 gain_source aeroengine5_throttle
 gain_factors -0.5 1.0
 sound 1000.0 default_pistonprop_hipower.wav
}

tracks/default_pistonprop_lopower6
{
 trigger_source always_on
 pitch_source aeroengine6_rpm
 gain_source aeroengine6_throttle
 gain_factors 0.5 0.5
 sound 1000.0 default_pistonprop_lopower.wav
}

tracks/default_pistonprop_hipower6
{
 trigger_source aeroengine6
 pitch_source aeroengine6_rpm
 gain_source aeroengine6_throttle
 gain_factors -0.5 1.0
 sound 1000.0 default_pistonprop_hipower.wav
}

tracks/default_pistonprop_lopower7
{
 trigger_source always_on
 pitch_source aeroengine7_rpm
 gain_source aeroengine7_throttle
 gain_factors 0.5 0.5
 sound 1000.0 default_pistonprop_lopower.wav
}

tracks/default_pistonprop_hipower7
{
 trigger_source aeroengine7
 pitch_source aeroengine7_rpm
 gain_source aeroengine7_throttle
 gain_factors -0.5 1.0
 sound 1000.0 default_pistonprop_hipower.wav
}

tracks/default_pistonprop_lopower8
{
 trigger_source always_on
 pitch_source aeroengine8_rpm
 gain_source aeroengine8_throttle
 gain_factors 0.5 0.5
 sound 1000.0 default_pistonprop_lopower.wav
}

tracks/default_pistonprop_hipower8
{
 trigger_source aeroengine8
 pitch_source aeroengine8_rpm
 gain_source aeroengine8_throttle
 gain_factors -0.5 1.0
 sound 1000.0 default_pistonprop_hipower.wav
}
``` 

### Marine (Large) 

```
tracks/default_marine_large
{
 trigger_source engine
 pitch_source engine_rpm
 sound 100.0 default_marine_large.wav
}
``` 

### Marine (Small)

```
tracks/default_marine_small
{
 trigger_source engine
 pitch_source engine_rpm
 sound 100.0 default_marine_small.wav
}
```
