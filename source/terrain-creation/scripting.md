Terrain Scripting
============

## Event box

this simple example will create an oil depot that reacts on trucks that drive into it.

### Prerequisites

-   move nhelens.zip to the  `Documents/My Games/Rigs of Rods/mods` folder and unpack all its files to a new directory "nhelens"
-   remove the old nhelens.zip to prevent collisions
-   Enable "Debug Collisions" in your RoR settings ('Settings'&gt;'Diagnostic'&gt;'Debug Collisions') to be able to see the debug visualization for events
-   get an oil-well mesh and a fitting .odef file: ~~<http://forumold.rigsofrods.com/index.php?topic=28551.msg355869#msg355869>~~ (Needs a new link)

### Defining the event box

Specified using following keywords:

* **boxcoords**: Size and position of the box, relatively to the position of the object.
* **virtual**: specifies that this box is an event box
* **event** [event_name] [event_type]:
  * **event_name**: the name of the box that the script will get when being notified.
  * **event_type**: valid eventTypes that trigger this: avatar, truck, airplane, delete.

Example:

    beginbox
    boxcoords 0.0, 20.0, 0.0, 5.0, -4.5, -0.5
    virtual
    event trigger truck
    endbox

### Programming the AngelScript file

-   create a file named <filename>.terrn.as, so in our case the file should be called `a1da0UID-nhelens.terrn.as` when the terrain we use is called `a1da0UID-nhelens.terrn`

```cpp
// Always include the base.as file!
#include "base.as"

string calledLast="";

void main()
{
    // spawn an oil-well
    game.spawnObject("oil-well", "my-oil-well-1", vector3(1119.44f, 33.933f, 924.982f), vector3(0, 0, 0), "myCallBack", false);
}

void myCallBack(int trigger_type, string inst, string box, int nodeid)
{
    if(calledLast == inst) return; // already triggered, discard

    // we log a message to the logfile
    log(inst + " event triggered");

    // We show a message ingame
    game.flashMessage(inst + " event triggered", 3, -1);

    calledLast = inst;
}
```

### Test-Run

you should see something like this:

![eventbox-debug1] ![eventbox-debug2]

[eventbox-debug1]: ../images/scripting-odef-eventbox-debug-1.jpg

[eventbox-debug2]: ../images/scripting-odef-eventbox-debug-2.jpg


note: We're only interested in the pink boxes here, as they represent event boxes. Light pink boxes do not call back an AngelScript function, while dark pink boxes do call back an AngelScript function when triggered (~when you drive into them).

if you do not see an oil loader, check the AngelScript.log file for errors. With no errors the log could read like this:

```
 ScriptEngine initialized
 ScriptEngine (SE) initializing ...
 Type registrations done. If you see no error above everything should be working
 ScriptEngine running
 saving script bytecode to file script_a1da0UID-nhelens.terrn.asc
 Executing main()
 The script finished successfully.
```

### Result

What happens if you drive a truck into the pink event box: 

[eventbox-oilrig]: ../images/scripting-odef-eventbox-oilrig.jpg

![eventbox-oilrig]

look at your AngelScript.log (on Windows, it's located under Documents\My Games\Rigs of Rods\logs):

    02:55:05: SE| my-oil-well-1 event triggered

### Whats next

you could:

-   check if the correct oil tanker trailer is in the spawn box
-   direct the user to the oil unloading station after "loading the oil" (sleeping) for some time
-   increase the node weight of a certain node inside of the tanker trailer to simulate the loaded oil.

### Advanced Examples

for example this script will create two oil rigs and will redirect the user to collect and drop oil between them:

```cpp
#include "base.as"

float timer = 0;
int timerSet = 0;

int state = 0;

vector3 pos_oil1(1099, 33.933, 924.982);
vector3 pos_oil2(1030, 33.4509, 1125.37);

void main()
{
    // spawn some oil-wells
    game.spawnObject("oil-well", "my-oil-well-1", pos_oil1, vector3(0, 0, 0), "callBackOilWellOne", false);
    game.spawnObject("oil-well", "my-oil-well-2", pos_oil2, vector3(0, 0, 0), "callBackOilWellTwo", false);
}

void frameStep(float dt)
{
    // count down the timer
    if(timer > 0)
        timer -= dt;
}

void callBackOilWellOne(int trigger_type, string inst, string box, int nodeid)
{
    //if(trigger_type != 1)  return; // we only want to trigger on events where the full truck is in the event box (doesn't work at the moment)
    if(state != 0) return; // only process this if state is valid
    
    if(timerSet == 0)
    {
        // set timer
        timerSet = 1;
        timer = 5;
        game.flashMessage("Loading oil ...", timer, -1);
        return;
    }
    
    if(timerSet == 1 && timer < 0)
    {
        // timer ran out, do something
        game.setDirectionArrow("unload oil", pos_oil2);
        state = 1;
        timerSet=0;
    }
}

void callBackOilWellTwo(int trigger_type, string inst, string box, int nodeid)
{
    //if(trigger_type != 1)  return; // we only want to trigger on events where the full truck is in the event box (doesn't work at the moment)
    if(state != 1) return; // only process this if state is valid
    
    if(timerSet == 0)
    {
        // set timer
        timerSet = 1;
        timer = 5;
        game.flashMessage("Unloading oil ...", timer, -1);
        return;
    }
    
    if(timerSet == 1 && timer < 0)
    {
        // timer ran out, do something
        game.setDirectionArrow("load some new oil", pos_oil1);
        state = 0;
        timerSet=0;
    }
}

```

## Adding a race to a terrain

In this tutorial, we will add a race to our terrain.

### How do races work?

In Rigs of Rods, races are added using a script file. The race that we will create in this tutorial will exist out of multiple checkpoints. The objective of the race is to get from the first till the last checkpoint as fast as possible.

We will discuss 2 methods to add a race to your terrain:

1.  Using a race script generator (fast method);
2.  Manually creating the script (advanced method).

### Adding a race (fast method)

You can find a race script generator [here](race-generator.md).

The checkpoints can be added by specifying the position (x,y,z), rotation (x,y,z) and an object for every checkpoint. This is similar to the [old .terrn file](old-terrn-subsystem.md) syntax, but be aware: do NOT add the checkpoint objects to the terrain using the [old .terrn file](old-terrn-subsystem.md). The objects will already be spawned by the script.

A checkpoint object is like every other object, but has beside a visible mesh also a virtual event box. The checkpoint will be marked as passed as soon as you drive through the virtual event box.

If you wish, you can also use the default objects, which are available by default in every Rigs of Rods installation. To use these, use objectname "chp-start" for the start and finish line and "chp-checkpoint" for the normal checkpoints. The race script generator will use these objects if you don't specify other objects.

After generating your race, you'll need to copy the script and put it in a new file in your terrain archive. The name of this file should be `terrainFileName.terrn.as`.
For example, for North Saint Helens, this would become: `a1da0UID-nhelens.terrn.as` because the terrain file name of North Saint Helens is `a1da0UID-nhelens.terrn`, and we just need to add `.as` to that.

### Adding a race (advanced method)

The easiest way to explain this method is by looking at some examples.

#### North Saint Helens

This example script is usable to add a race to the North Saint Helens terrain (a1da0UID-nhelens.terrn).

Every line that starts with '//' is information that explains the line(s) beneath it.

File: a1da0UID-nhelens.terrn.as

```cpp
// The following line is required in every script, in order to ensure that
// the spawnpoints keep working. It includes the script inside the file "base.as" here.

#include "base.as"

// We want to add a race, so we will need the race script.

#include "races.as"

// We need to initialize the race script.

racesManager races();

// Here we start the main function. 
// A function called 'main' will get called as soon as the terrain has completed loading. 
// So inside this function is a perfect spot to tell the game about our races. 

void main() {

   // We change an option of the races script
   //    Because of the scattered nature of this race, we want to make sure that
   //    the user finds his way to the start line of the race.
   //    So, by setting this option to 'true', we make sure that when the user
   //    passes a checkpoint when not in a race, the user will still get a
   //    message informing the user about the race.
   races.showCheckPointInfoWhenNotInRace = true;
   
   // For the game to recognize the race, it needs to know where the checkpoints are,
   //    so we define them in an Array.
   //    Every line with numbers defines a checkpoint.
   //    The numbers on a line are from left to right: position X, Y, Z, rotation X, Y, Z
   //    (with position in meters and rotation in degrees)
   //    So they're coordinates to uniquely define the location and rotation of an
   //    object in a three dimensional space.
   array<array<double>> coordinates = 
       {
           // { pos X  ,  pos Y   ,   pos Z     ,  rot X  ,   rot Y   ,  rot Z  }
           {1145.762451, 43.409168,  1874.828247, 0.000000, -20.000000, 0.000000},
           {1223.362061, 66.093338,  2128.568359, 0.000000, 30.000000,  0.000000},
           {1493.947388, 90.977753,  2490.836426, 0.000000, 55.000000,  0.000000},
           {1854.234497, 141.551270, 2732.894287, 0.000000, 65.000000,  0.000000},
           {2157.161865, 130.438171, 2720.815430, 0.000000, 90.000000,  0.000000},
           {2422.710693, 110.228294, 2523.404785, 0.000000, 140.000000, 0.000000},
           {2607.359619, 107.782913, 2203.569824, 0.000000, 165.000000, 0.000000},
           {2534.100342, 107.596176, 1938.718140, 0.000000, 205.000000, 0.000000},
           {2269.411377, 134.870911, 1729.099121, 0.000000, 265.000000, 0.000000},
           {1974.688110, 104.931290, 1732.083618, 0.000000, 245.000000, 0.000000},
           {1865.982056, 101.138504, 1618.693237, 0.000000, 245.000000, 0.000000},
           {1706.379395, 148.594437, 1533.436157, 0.000000, 255.000000, 0.000000},
           {1470.152100, 120.901085, 1504.998291, 0.000000, 310.000000, 0.000000},
           // Note: No comma after the last checkpoint.
           {1238.410767, 47.336208,  1735.698242, 0.000000, 325.000000, 0.000000}
       };
   
   // Now we add the race with name 'Rigbreaker'.
   // The last parameter is number of laps.
   // * This race has 1 lap.
   // * You can use 'races.LAPS_NoLaps' to have no laps 
   //       (~the race start point is not the same checkpoint as the race finish point).
   // * You can also use 'races.LAPS_Unlimited' to have a never ending race (~unlimited amount of laps)
   races.addRace("Rigbreaker", coordinates, 1);

} // end of the main function

// The default RoR event callback
// This procedure will get called by Rigs of Rods on certain occasions,
// decided by the race script. 
void eventCallback(int eventnum, int value) {

   // It's not obligated to add this, but it's a good habit.
   races.eventCallback(eventnum, value);

}

// end of the script. 

```

#### Island

This example script is usable to add a race to the Island terrain (496aUID-island.terrn).

File: 496aUID-island.terrn.as

```cpp
#include "base.as"
#include "races.as"

racesManager races();

// The default RoR main function 
void main() {

   array<array<double>> coordinates = {
       {791.551, 87.6567, 1558.25, 0.0,  35.3333, 0.0},
       {970.905, 119.2  , 1421.01, 0.0, -93.6470, 0.0},
       {1350.28, 157.644, 1375.19, 0.0, -44.4060, 0.0},
       {1506.18, 180.185, 1309.12, 0.0,  29.4644, 0.0},
       {1306.9 , 209.358, 1250.37, 0.0,  70.3679, 0.0},
       {940.346, 236.788, 926.603, 0.0,  16.9539, 0.0}
   };
   races.addRace("To The Top", coordinates, races.LAPS_NoLaps);
}

// The default RoR event callback
void eventCallback(int eventnum, int value) {

   races.eventCallback(eventnum, value);

}

```

#### Bajarama

This example script shows a race with an unlimited amount of laps (a never ending race). It is usable with the Bajarama terrain (8c07UID-bajarama.terrn).

File: 8c07UID-bajarama.terrn.as 

```cpp
#include "base.as"
#include "races.as"

racesManager races();

void main() {

   array<array<double>> coords1 = {
       {179.088196,     1.351834,   203.319107,    -0.000006,    75.500044,    -0.849956},
       {56.070511,      1.247547,   119.811401,     0.000001,   109.500097,     1.700087},
       {88.742783,      2.674362,   332.812042,     0.000071,   127.500016,    -7.299959},
       {157.537796,     1.121414,   478.227203,     0.595164,   -29.497634,    -0.456070},
       {202.784286,     1.830205,   240.792023,     0.446688,   -87.490632,    -2.408985},
       {326.742004,     1.115725,   436.851685,     0.000000,     0.000003,    -0.200001},
       {360.338379,     1.100020,   102.170441,     0.000033,  -140.500010,    -0.700087},
       {482.216766,     1.089854,   430.449249,     0.000000,     0.000000,    -0.500001},
       {478.902618,     1.325789,    90.371094,     0.000000,    -0.000014,     0.000000},
       {92.562027,      1.122820,    86.679283,     0.000002,   -91.000017,     0.000002},
       {264.193359,     1.481601,   121.791405,     0.000000,  -179.999991,    -0.700000}
   };
   //                           race name coordinates   #laps          checkpoint object     startline object
   int raceID = races.addRace("Bajarama", coords1, races.LAPS_Unlimited, "new-checkpoint", "new-checkpoint-start");

}

// The default RoR event callback
void eventCallback(int eventnum, int value) {

   races.eventCallback(eventnum, value);

}

```

#### Flat Map (v10.1)

This example script illustrates how to add multiple races to one terrain and is usable for the Flat Map terrain (f4afUID-flat_map_full32xa.terrn).

File: f4afUID-flat_map_full32xa.terrn.as

```cpp
#include "base.as"

#include "races.as"

racesManager races();

void main() {

    // We add 4 races to the map
    // RACE 1: Dirt drag race - right side
    array`<array<double>`> coords1 = {
        {2293.272705, 0.0, 2035.251465, 0.0, 0.0, 0.0},
        {2293.272705, 0.0, 1484.145752, 0.0, 0.0, 0.0}
    };
    //                              race name           coordinates   #laps
    int raceID = races.addRace("Dirt DragRace - Right Side", coords1, races.LAPS_NoLaps);
    // race 1 added and working

    // RACE 2: Dirt drag race - left side
    array`<array<double>`> coords2 = {
        {2268.944580, 0.0, 2035.251465, 0.0, 0.0, 0.0},
        {2268.944580, 0.0, 1484.145752, 0.0, 0.0, 0.0}
    };
    //                              race name           coordinates   #laps
    int raceID = races.addRace("Dirt DragRace - Left Side", coords2, races.LAPS_NoLaps);
    // race 2 added and working

    // RACE 3: Runway drag race - left side
    array`<array<double>`> coords3 = {
        {2327.494141, 1.0, 1388.388794, 0.0, 0.0, 0.0},
        {2327.494141, 1.0, 932.558044 , 0.0, 0.0, 0.0}
    };
    //                              race name           coordinates   #laps
    int raceID = races.addRace("Runway DragRace - Left Side", coords3, races.LAPS_NoLaps);
    // race 3 added and working

    // RACE 4: Runway drag race - right side
    array`<array<double>`> coords4 = {
        {2343.309814, 1.0, 1388.388794, 0.0, 0.0, 0.0},
        {2343.309814, 1.0, 932.558044 , 0.0, 0.0, 0.0}
    };
    //                              race name           coordinates   #laps
    int raceID = races.addRace("Runway DragRace - Right Side", coords4, races.LAPS_NoLaps);
    // race 4 added and working

}

// The default RoR event callback 

void eventCallback(int eventnum, int value) {

    races.eventCallback(eventnum, value);

}
```

#### F1 Test Track

This example script illustrates how to use custom checkpoint objects and multiple races on one terrain. The script can be used with the F1 Test Track terrain (2af11UID-f1_testtrack.terrn).

File: 2af11UID-f1_testtrack.terrn.as 

```cpp
#include "base.as"

#include "races.as"

racesManager races();

// The default RoR main function 
void main() {

    // We add 5 races to the map

    // RACE 1
    array<array<double>> coords1 = {
            { 882.132996,    0.120613,  1324.317139,    0.0,    90.0,    0.0},
            { 658.905884,    0.076029,  1324.323730,    0.0,    90.0,    0.0},
            { 575.903259,    0.062041,  1231.623169,    0.0,     0.0,    0.0},
            { 565.184814,    0.063519,  1037.515503,    0.0,    22.0,    0.0},
            { 313.121979,    0.079952,   822.904663,    0.0,     5.0,    0.0},
            { 385.599213,    0.071390,   722.493469,    0.0,   -90.0,    0.0},
            { 770.934998,    0.012638,   761.321411,    0.0,   -90.5,    0.0},
            {1055.889404,    0.078151,   664.507324,    0.0,   -89.0,    0.0},
            {1388.452026,    0.030632,   663.976257,    0.0,    92.0,    0.0},
            {1457.364014,    0.041678,   783.509460,    0.0,   168.0,    0.0},
            {1493.774048,    0.104160,  1309.505859,    0.0,    18.5,    0.0},
            {1348.787964,    0.099335,  1324.566406,    0.0,    90.0,    0.0},
            { 909.298462,    0.044833,  1324.610596,    0.0,    88.5,    0.0}
        };
    //                              race name    coordinates   #laps         checkpoint object     startline object        finishline object
    int raceID = races.addRace("Grand Prix long", coords1, races.LAPS_NoLaps, "new-checkpoint", "new-checkpoint-start", "new-checkpoint-start");
    // race 1 added and working

    // RACE 2
    array<array<double>> coords2 = 
        {
            {1176.429688,    0.063195,  1254.195313,    -0.0,    90.0,    0.0},
            { 693.874573,    0.090642,  1251.470825,    -0.0,    90.0,    0.0},
            { 693.383728,    0.071324,  1182.933594,    -0.0,   -90.0,    0.0},
            { 844.552612,    0.095163,  1168.225586,    -0.0,   -90.0,    0.0},
            { 941.776978,    0.052285,  1183.067139,    -0.0,   -90.0,    0.0},
            {1079.778198,    0.096842,  1183.057373,    -0.0,   -90.0,    0.0},
            {1177.627563,    0.067999,  1125.772461,    -0.0,   -40.0,    0.0},
            {1282.897095,    0.938393,  1045.571899,     0.0,   -90.0,    0.0},
            {1395.055054,    0.107390,  1148.677734,    -0.0,     0.0,    0.0},
            {1290.430908,    0.098327,  1254.477905,     0.0,    90.0,    0.0}
        };
    //                          race name    coordinates   #laps         checkpoint object     startline object        finishline object
    raceID = races.addRace("Grand Prix short", coords2, races.LAPS_NoLaps, "new-checkpoint", "new-checkpoint-start", "new-checkpoint-start");
    // race 2 added and working

    // RACE 3
    array<array<double>> coords3 =
        {
            {1117.230103,     0.067576,   700.704956,    0.0,   -90.0,    0.0},
            {1136.480469,     0.072812,  1030.468628,    0.0,    90.0,    0.0},
            {1101.686768,     0.032589,   701.005127,    0.0,   -90.0,    0.0}
        };
    //                       race name    coordinates   #laps         checkpoint object     startline object        finishline object
    raceID = races.addRace("oval race", coords3, races.LAPS_NoLaps, "new-checkpoint", "new-checkpoint-start", "new-checkpoint-start");
    // race 3 added and working

    // RACE 4
    array<array<double>> coords4 = 
        {
            {1187.875977,     0.0,       1220.567383,    0.0,    90.0,    0.0},
            { 784.379578,     0.0,       1221.171143,    0.0,   -90.0,    0.0}
        };
    //             race name    coordinates   #laps         checkpoint object     startline object        finishline object       race version
    raceID = races.addRace("drag race", coords4, races.LAPS_NoLaps, "new-checkpoint", "new-checkpoint-start", "new-checkpoint-start");
    // race 4 added and working

    // RACE 5
    double[][] coords5 = 
        {
            //   x        z          y      3d rot    rot     3d rot
            { 807.868, 5.09987,   1114.47,    0.0,   -90.0,    0.0},
            { 724.386, 0.0994606, 1084.16,    0.0,     0.0,    0.0},
            { 718.647, 0.0998037, 1038.22,    0.0,    45.0,    0.0},
            { 696.235, 0.0989883,  992.215,   0.0,   -25.0,    0.0},
            { 754.302, 0.098882,   999.441,   0.0,     0.0,    0.0},
            { 763.464, 0.0987995, 1049.56,    0.0,    45.0,    0.0},
            { 831.675, 5.01375,   1058.26,    0.0,    90.0,    0.0},
            { 919.557, 0.0995347, 1083.47,    0.0,     0.0,    0.0},
            { 884.884, 0.0987005, 1121.12,    0.0,   -90.0,    0.0}
        };
    //                   race name   coordinates   #laps (no checkpoint objects are specified here, so the default RoR ones will be used)
    raceID = races.addRace("mud race", coords5, 3);
    // race 5 added and working

}

// The default RoR event callback 
void eventCallback(int eventnum, int value) {

    races.eventCallback(eventnum, value);

}
```

#### F1 Test Track (with penalty events)

We can also penalty events if the player hits a specific part of the checkpoint.

For this race, we've edited the 2af11UID-new-checkpoint.odef file 
from [f1track_improved.zip](https://cdn.anotherfoxguy.com/repo-backup/c1ae6cfbb628afe6e81c511ac8ac65e2a7bddae1_f1track_improved.zip) 
to have penalty event boxes: 

```ini
2af11UID-new-checkpoint.mesh 1, 1, 1

beginbox boxcoords -7.5, 6.95, -4.0, 5.2, -0.5, 0.5 virtual event checkpoint truck endbox

beginbox boxcoords -8.6, -7.65, 0.0, 0.55, -0.65, 0.0 virtual event race_penalty truck endbox

beginbox boxcoords 8.05, 7.1, 0.0, 0.55, -0.65, 0.0 virtual event race_penalty truck endbox

end
```
So the checkpoint looks like this (in debug mode): \[image to be added here\]

As you can see, there are 2 small event boxes that will trigger the penalty event. The penalty event will, when triggered, add an amount of seconds to the lap time. How many seconds can be configured using the [races.setPenaltyTime(int raceID, int seconds)](https://developer.rigsofrods.org/d9/dce/class_script2_script_1_1races_manager.html#a6d33d12db6fe5798ee9579aab701206d) method or you can just change it using the PenaltyEvent callback function.

We'll also need this PenaltyEvent callback function when we want to show a message if a penalty event was triggered. For this we'll need to:

1.  Define the callback function ('on_penaltyEvent' in the script below)
2.  Tell the races script about this callback function ('races.setCallback("PenaltyEvent", on_penaltyEvent);')

This is all done in the following script. Pay attention to every difference with the script above.

```cpp
#include "base.as"
#include "races.as"

racesManager races();

// The default RoR main function 

void main() {

    // the penalty event shows no message by default, so we'll have to show a message ourself. 
    races.setCallback("PenaltyEvent", on_penaltyEvent); 

    // We add 5 races to the map 
    // RACE 1 
    array <array<double> > coords1 = { 
            { 882.132996,    0.120613,  1324.317139,    0.0,    90.0,    0.0}, 
            { 658.905884,    0.076029,  1324.323730,    0.0,    90.0,    0.0}, 
            { 575.903259,    0.062041,  1231.623169,    0.0,     0.0,    0.0}, 
            { 565.184814,    0.063519,  1037.515503,    0.0,    22.0,    0.0}, 
            { 313.121979,    0.079952,   822.904663,    0.0,     5.0,    0.0}, 
            { 385.599213,    0.071390,   722.493469,    0.0,   -90.0,    0.0}, 
            { 770.934998,    0.012638,   761.321411,    0.0,   -90.5,    0.0}, 
            {1055.889404,    0.078151,   664.507324,    0.0,   -89.0,    0.0}, 
            {1388.452026,    0.030632,   663.976257,    0.0,    92.0,    0.0}, 
            {1457.364014,    0.041678,   783.509460,    0.0,   168.0,    0.0}, 
            {1493.774048,    0.104160,  1309.505859,    0.0,    18.5,    0.0}, 
            {1348.787964,    0.099335,  1324.566406,    0.0,    90.0,    0.0}, 
            { 909.298462,    0.044833,  1324.610596,    0.0,    88.5,    0.0} 
        }; 
    //                              race name    coordinates   #laps         checkpoint object     startline object        finishline object 
    int raceID = races.addRace("Grand Prix long", coords1, races.LAPS_NoLaps, "new-checkpoint", "new-checkpoint-start", "new-checkpoint-start"); 
    races.setPenaltyTime(raceID, 10); //  <- this sets the default penalty time (in seconds) for this race when a race_penalty event occurs.
    // race 1 added and working
 
 
    // RACE 2
    array<array<double> > coords2 =  
        { 
            {1176.429688,    0.063195,  1254.195313,    -0.0,    90.0,    0.0}, 
            { 693.874573,    0.090642,  1251.470825,    -0.0,    90.0,    0.0}, 
            { 693.383728,    0.071324,  1182.933594,    -0.0,   -90.0,    0.0}, 
            { 844.552612,    0.095163,  1168.225586,    -0.0,   -90.0,    0.0}, 
            { 941.776978,    0.052285,  1183.067139,    -0.0,   -90.0,    0.0}, 
            {1079.778198,    0.096842,  1183.057373,    -0.0,   -90.0,    0.0}, 
            {1177.627563,    0.067999,  1125.772461,    -0.0,   -40.0,    0.0}, 
            {1282.897095,    0.938393,  1045.571899,     0.0,   -90.0,    0.0}, 
            {1395.055054,    0.107390,  1148.677734,    -0.0,     0.0,    0.0}, 
            {1290.430908,    0.098327,  1254.477905,     0.0,    90.0,    0.0} 
        }; 
    //                          race name    coordinates   #laps         checkpoint object     startline object        finishline object 
    raceID = races.addRace("Grand Prix short", coords2, races.LAPS_NoLaps, "new-checkpoint", "new-checkpoint-start", "new-checkpoint-start"); 
    races.setPenaltyTime(raceID, 10); //  <- this sets the default penalty time (in seconds) for this race when a race_penalty event occurs.
    // race 2 added and working
 
 
    // RACE 3
    array<array<double> > coords3 =  
        { 
            {1117.230103,     0.067576,   700.704956,    0.0,   -90.0,    0.0}, 
            {1136.480469,     0.072812,  1030.468628,    0.0,    90.0,    0.0}, 
            {1101.686768,     0.032589,   701.005127,    0.0,   -90.0,    0.0} 
        }; 
    //                       race name    coordinates   #laps         checkpoint object     startline object        finishline object 
    raceID = races.addRace("oval race", coords3, races.LAPS_NoLaps, "new-checkpoint", "new-checkpoint-start", "new-checkpoint-start"); 
    races.setPenaltyTime(raceID, 10); //  <- this sets the default penalty time (in seconds) for this race when a race_penalty event occurs.
    // race 3 added and working
 
 
    // RACE 4
    array<array<double> > coords4 =  
        { 
            {1187.875977,     0.0,       1220.567383,    0.0,    90.0,    0.0}, 
            { 784.379578,     0.0,       1221.171143,    0.0,   -90.0,    0.0} 
        }; 
    //             race name    coordinates   #laps         checkpoint object     startline object        finishline object       race version 
    raceID = races.addRace("drag race", coords4, races.LAPS_NoLaps, "new-checkpoint", "new-checkpoint-start", "new-checkpoint-start"); 
    races.setPenaltyTime(raceID, 10); //  <- this sets the default penalty time (in seconds) for this race when a race_penalty event occurs.
    // race 4 added and working
 
 
    // RACE 5
    double[][] coords5 = 
        {
            //   x        z          y      3d rot    rot     3d rot
            { 807.868, 5.09987,   1114.47,    0.0,   -90.0,    0.0},
            { 724.386, 0.0994606, 1084.16,    0.0,     0.0,    0.0},
            { 718.647, 0.0998037, 1038.22,    0.0,    45.0,    0.0},
            { 696.235, 0.0989883,  992.215,   0.0,   -25.0,    0.0},
            { 754.302, 0.098882,   999.441,   0.0,     0.0,    0.0},
            { 763.464, 0.0987995, 1049.56,    0.0,    45.0,    0.0},
            { 831.675, 5.01375,   1058.26,    0.0,    90.0,    0.0},
            { 919.557, 0.0995347, 1083.47,    0.0,     0.0,    0.0},
            { 884.884, 0.0987005, 1121.12,    0.0,   -90.0,    0.0}
        };
    //                   race name   coordinates   #laps (no checkpoint objects are specified here, so the default RoR ones will be used)
    raceID = races.addRace("mud race", coords5, 3);
    // race 5 added and working
}
 
// The default RoR event callback
void eventCallback(int eventnum, int value)
{
    races.eventCallback(eventnum, value);
}

void on_penaltyEvent(dictionary@ info)
{
    // this method gets called every time a race_penalty event occurs.
        
    // We can also change the penalty time here:
    info.set("penaltyTime", 10);
    // But the penalty time was already set to 10 seconds, because we had set it to 10 in the main() function.
    // So now we've set it twice to 10 seconds, which is quite pointless...
        
    // Just show a message to inform the user about the penalty
    races.message("PENALTY", "lightning.png");
}

```

**Notes:**

1.  We've only used the 'race_penalty' event here, but you can also use the 'race_abort' event, which will abort the race when the event box is triggered.
2.  Another way to add penalty seconds is using the [races.addPenaltySeconds(int seconds)](https://developer.rigsofrods.org/d9/dce/class_script2_script_1_1races_manager.html#a6d33d12db6fe5798ee9579aab701206d) method.
3.  You can also register callback functions for other events: <https://developer.rigsofrods.org/d9/dce/class_script2_script_1_1races_manager.html>

## More Advanced Functionality

### Documentation and questions

See [reference manual](https://developer.rigsofrods.org/d2/d42/group___script_side_a_p_is.html). Studying the script files of other terrains may also greatly help you.

In case of questions/suggestions/complains, get in touch [in the forums](https://forum.rigsofrods.org/forums/development-discussions.6/).

### Example: Extending RacesManager

Here's an example where we inherit from the racesManager class and add functionality. (In this case, we limit the allowed vehicles, so the race won't start if certain vehicles aren't used). You can test this script by adding it to the North Saint Helens terrain.

```cpp
#include "base.as";
#include "races.as";

racesManagerWithVehicleLimit races();

void main() {

    // Add the race like usual  
    array < array<double>  > coords1 = {  
        {1140.259644, 34.136135, 920.070313, 0.0, 0.0, 0.0},  
        {1140.259644, 34.136135, 950.070313, 0.0, 0.0, 0.0}  
    };  
    int raceID_testRace = races.addRace("testRace", coords1, races.LAPS_NoLaps);  
      
    // Add some vehicles (when you don't add any vehicles, then all vehicles will be allowed)  
    races.addVehicle(raceID_testRace, "Bus RVI agora S");  
    races.addVehicle(raceID_testRace, "Bus RVI agora L");  

}

// Other stuff (No race specific stuff under this line)

class racesManagerWithVehicleLimit : racesManager {

    dictionary vehicleData;  
    double lastMessageTime;  
      
    racesManagerWithVehicleLimit()  
    {  
        super();  
        lastMessageTime = 0.0;  
    }  

    // extend this method  
    void startRace(int raceID) /*override*/  
    {  
        bool allow = true;  
      
        // Do we have vehicle data for this race?  
        array <string> @ vehicles = null;  
        if(vehicleData.get("race_"+raceID, @vehicles))  
        {  
            // Get the name of the current truck  
            string truckName = "avatar";  
            BeamClass@ truck = game.getCurrentTruck();  
            if(truck !is null)  
                truckName = truck.getTruckName();  

            if(vehicles.find(truckName) <0) 
                allow = false; 
        } 
         
        if(allow) 
            racesManager::startRace(raceID); 
        else  
        { 
            // Avoid message spam (in exceptional cases) 
            if((game.getTime()-this.lastMessageTime)> 5.0)  
            {  
                this.lastMessageTime = game.getTime();  
              
                this.message("Race "+this.raceList[raceID].raceName+" can only be started with one of the following vehicles:", "information.png");  
                this.message(arrayToString(vehicles), "information.png");  
            }  
        }  
    }  
      
    void addVehicle(int raceID, string vehicleName)  
    {  
        array <string> @ vehicles = null;  
        if(!vehicleData.get("race_"+raceID, @vehicles))  
        {  
            array <string>  vehicles2 = {};  
            @vehicles = @vehicles2;  
            vehicleData.set("race_"+raceID, @vehicles);  
        }  
          
        vehicles.insertLast(vehicleName);  
    }  

}

string arrayToString(array<string>@ arr) {

    string result = "";  
    if(arr !is null) for(uint i=0; i<arr.length(); ++i)  
    {  
        result += arr[i];  
        if(i!=arr.length()-1) result += ", ";  
    }  
    return result;  

}

```

### Troubleshooting

If your race doesn't work, feel free to post your terrain file in this forum, and we may have a look at it. <https://forum.rigsofrods.org/forums/content-support.10/>
