---
layout: page
title:  "Making softbody objects"
categories: [vehicle-creation]
---


This is an introduction and overview of making a softbody object (also called "nodebeam", or shortly "N/B") in Rigs of Rods. It may be vehicles of any sort, trailers, loads or any other objects. Since most of our softbody actors are vehicles, specifically heavy land vehicles, this documentation is included under "Vehicle creation".

To make trucks in Rigs of Rods, you need to understand how the game functions. Rigs of Rods simulates vehicles by connecting nodes via beams. Nodes are simply points in space. Beams are what connect nodes together.

Vehicles are specified using [truck file format](/technical/fileformat-truck). You can edit it using Notepad, Wordpad, or a basic text editor of your choice. Be prepared to devote a chunk of time to learning the syntax and testing your vehicle!

# Planning

It is wise to plan your truck before you begin your work in RoR. Things to keep in mind:

-    How many wheels will you have?
-    Which kind of geometry (cubic or prismatic) ?
-    How many truss group? 

Often you build a strong chassis base that supports a cab structure, lowers the center of gravity, and deforms realistically in impact. The most practical chassis structure is a cubic structure with three cell groups. The cubic is heavier than the prismatic, but is easier to integrate (for a cubic example see the TurboTwin truck, and for the prismatic see the Wrecker truck). Other arrangements are possible, you can try whatever you want.

A good chassis is **strong**, **light** (less nodes, more frames per second) and is **modular** so that other parts of the vehicle can be attached (cab, suspensions, loads, and etc.).

## The draft

This example will walk through a minimalistic design: a single-cell cubic structure, with three segments. It is a good idea to start out simple, as a complex design can lead to frustration.

![](/images/softbody-tutorial-soapbox-draft.jpg)

Yes, we are going to do this sorry piece of soapbox... ;-)

## The Blueprint

Now that we know the big picture, we do a scaled plan of the truck. Using drawing paper and a pen saves a lot of time, and is **very important** for the next steps, because the drawing will serve as a reference for nodes, and having this sheet of paper under the keyboard helps a lot! This is also the time to find the dimensions (1.00 unit in RoR = 1 meter) of the truck.

Draw the left side view (up) and top view (down), position the nodes, and number them. Generally, nodes overlap each over so number the overlapped nodes by separating them with a horizontal bar. We will do the chassis first, so I numbered only the chassis nodes for the moment.

![](/images/softbody-tutorial-soapbox-blueprint.jpg)

Notice the reference vectors:

-    X is front to back
-    Y id bottom to top
-    Z right to left 

# The truck file

Create a text file in the _MyDocuments\Rigs of Rods XX\vehicles_ directory. Call it _tutorial.truck_.

## Required sections

Not including certain sections can yield different results, from making the vehicle explode upon spawning, to its nonappearance in the selection menu.

The first line MUST begin with the truck name:

    Tutorial Truck
    
Then the globals section, containing the dry mass (in this case, 10 metric tons), the load mass (zero, no loaded nodes) and any pre-existing material name (don't need this yet). 

    globals
    10000.0, 0.0, tracks/semi

Then add the nodes, with the coordinates from the drawn plan, and the beams. The beams section has "structural" beams that follow the cubic structure, and the "reinforcement" beams that triangulates and strengthens the structure. This separation helps to debug in case of errors.

After adding the nodes, define some points of reference on the chassis with the cameras and cinecam sections. The first takes a reference node (any node will do), a node straight behind and a node straight left. The second takes the coordinates of the internal camera, and 8 attach nodes. This gives: 

    cameras
    2,6,0

    cinecam
    ;x,y,z,bindings
    0.5, 0.5, 1.0, 0,1,2,3,4,5,6,7
    
## Nodes and Beams

Don't forged nodes are perfect ball joints, not shaped connectors. If you create a box of only structural beams, it will fold. You need to add reinforcements.

[rigidity-box1]:   /images/softbody-rigidity-tutorial-box1.png
{: width="40%"}
[rigidity-box2]:   /images/softbody-rigidity-tutorial-box2.png
{: width="40%"}

![rigidity-box1] ![rigidity-box2]
    
Here is the resulting file:

    Tutorial truck

    globals
    10000.0, 0.0, tracks/semi

    nodes
    ;id,x,   y,   z
    0, 0.0, 1.0, 2.0
    1, 0.0, 0.0, 2.0
    2, 0.0, 1.0, 0.0
    3, 0.0, 0.0, 0.0
    4, 1.0, 1.0, 2.0
    5, 1.0, 0.0, 2.0
    6, 1.0, 1.0, 0.0
    7, 1.0, 0.0, 0.0
    8, 3.0, 1.0, 2.0
    9, 3.0, 0.0, 2.0
    10, 3.0, 1.0, 0.0
    11, 3.0, 0.0, 0.0
    12, 4.0, 1.0, 2.0
    13, 4.0, 0.0, 2.0
    14, 4.0, 1.0, 0.0
    15, 4.0, 0.0, 0.0

    beams
    ;main chassis
    ;structural
    0,1
    2,3
    4,5
    6,7
    8,9
    10,11
    12,13
    14,15

    0,4
    1,5
    2,6
    3,7
    4,8
    5,9
    6,10
    7,11
    8,12
    9,13
    10,14
    11,15

    0,2
    1,3
    4,6
    5,7
    8,10
    9,11
    12,14
    13,15

    ;reinforcements
    0,6
    1,7
    2,4
    3,5
    4,10
    5,11
    6,8
    7,9
    8,14
    9,15
    10,12
    11,13

    0,5
    1,4
    2,7
    3,6
    4,9
    5,8
    6,11
    7,10
    8,13
    9,12
    10,15
    11,14

    0,3
    1,2
    4,7
    5,6
    8,11
    9,10
    12,15
    13,14

    cameras
    2,6,0

    cinecam
    ;x,y,z,bindings
    0.5, 0.5, 1.0, 0,1,2,3,4,5,6,7

Here is the chassis rendered in RoR: 
    
![](/images/softbody-tutorial-soapbox-hull-ingame.jpg)

# Weight tuning

Making a stable, lightweight, and complex vehicle is a difficult challenge in RoR.  
You will certainly run into this problem if you try to do a light airplane (any airplane less than about 20 tons).

The root problem is that strong beams attached to light nodes are physically unstable. 
In RoR physics, only nodes bear weight. To ensure a realistic distribution of weight, the node weights are computed as this:

* Compute the sum of the length of all beams
* From the global net weight, compute the linear density of beams (total mass/total length)
* For each node, set its weight as the sum of the weight of all beams attached to it 
  (in fact, half the weight of the beams, to avoid double counting weight)
* Add extra load weight to the loaded nodes (the total load is divided by the number of nodes declared as loaded)
* Fix weight of ropes, hooks, and cameras to predefined "stable" values
* To ensure stability of all nodes, if a node is found to be below 50kg, its weigh is set to 50kg 
  (this can happen if a node is only connected to very short beams)

At the end of the process, the final, total mass of the vehicle can be higher than anticipated, 
especially if the last rule applied to a lot of nodes. With this rule, a 100 node 
vehicle can never be below 5 tons. Note that wheel node weights are computed separately depending on the wheel weight settings.

To know if your vehicle has gained weight, enabled mass debugging in the Configurator 
and load the vehicle into RoR.  Leave and look in RoR.log and check the last line 
"TOTAL VEHICLE MASS". This is the final total mass (including wheels).

If it is too much, you will need to lower the minimum node mass setting. 
You can do it with the "minimass" command (at the beginning of the truck/boat/airplane file):

    minimass
    25.0

You can also lower the global mass, to reduce the mass of "heavy" nodes (those not concerned by the minimum mass rule).

When you lower minimass, you will encounter physics instability. 
The solution to instability is to lower the rigidity of beams, using 
the "set_beam_defaults" to soften them until they are stable with the new mass settings.

But when you lower the rigidity, parts of the vehicle will be too fragile. 
So use set_beam_defaults to adjust strength depending on the stress elements will bear. 
For example, landing gear beams will need stronger beams, and fuselage softer beams.
You can also use loaded nodes to balance and/or stabilize specific unstable nodes.

So with the minimass and set_beam_defaults commands, with much guessing, 
trimming, and luck you can achieve lightweight airplanes.

