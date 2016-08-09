---
title: "Flares (how to add lights)"
layout: page
categories: [vehicle-creation]
---

<div class="toc" markdown="1">
  * TOC
  {:toc}
</div>

Before we begin, we need to ensure some basic understanding of flares, nodes, and planes (no, not the flying type). 

**The Definition of a Flare** Flares are basically lights that originate 
from a set of chosen nodes, which can be manipulated via the appropriate 
values in the .truck, .load, .trailer, .boat or .plane file. 
There are multiple types of flares, ranging from brake lights, 
to turn signals, to headlights, to specialty lighting. 

**The Coordinate Plane** Flares operate on a different coordinate plane than nodes, 
for some reason. Note these changes: 

<table style="margin: 1em auto">
<tr>
<th> Axis
</th>
<th> Chassis (N/B)
</th>
<th> Flares
</th></tr>
<tr>
<td> X
</td>
<td> Front to back
</td>
<td> Left to right
</td></tr>
<tr>
<td> Y
</td>
<td> Up to down
</td>
<td> Up to down
</td></tr>
<tr>
<td> Z
</td>
<td> Left to right
</td>
<td> Front/Back
</td></tr></table>

**Time Warning** Furthermore, be advised that adding flares to a vehicle 
will sometimes take quite a bit of time, depending on the type of vehicle, 
number of nodes, number of flares, etc. You've been warned. 

# Preparing the chassis

Before we begin, you'll absolutely need a truck editor, such as the [[tools/editorizer]], 
 This will allow you to see where each node is placed in relationship to the coordinate plane (X,Y,Z). 

Once the editor is running, and is open to the truck of your choice 
(it's suggested&nbsp;that one starts out with something simple, 
such as the old Cartrailer.load, which can be found on the repository), 
you'll need to select the checkbox up at the top that says, "Print Node Numbers." 
This is pretty self-explanatory, as you'll need three node numbers later on to add your flares. 

This next step can be challenging, depending on how many nodes and beams are present on the selected vehicle. 
You'll need to find three nodes close to where you want them on the vehicle. 
If you're adding brake/turn/head lights, it's suggested that you start with 
the lower lefthand corner of the front or back chassis, writing that node number 
on a piece of paper (this'll be your reference or REF node), 
then write down the node directly above it (this'll be your Y), and then finally, 
write the number of the node directly to the right of it (this'll be your X). 

<a href="/images/flares-finding-nodes.jpg"><img src="/images/flares-finding-nodes.jpg"></a>

If you cannot find REF,X,Y nodes because they aren't where you want the lights 
(e.g. you're working on the school bus, which has the tail lights quite a bit above the bumper), 
you can add three nodes, in the same fashion as noted above, and use them to base your flares off of, 
but that's too advanced to go in this tutorial. 

# Getting to Know Notepad 

Next up is man's best friend--the Windows notepad. If you're using another operating system, 
and/or another editor, that's fine, as long as it can save in ANSI format--it'll save you problems later on. 
Whatever you do, do not use MS Word/Wordpad/OpenOffice/AbiWord etc.

You'll need to open up the vehicle or load of choice with the aforementioned application 
(notepad or compliant editor). Here, you'll need to add a [[technical/fileformat-truck#flares flares]] section 

Once the line "flares" is added, you'll need to hit enter once, starting a new section, where it's advised you paste the syntax: 

    flares
    ;RefNode,X,Y,OffsetX,OffsetY, Type, ControlNumber, BlinkDelay, size MaterialName


# Tutorial

So imagine a flat plane with 4 nodes, the direction of the planes face up, down, left or right determines where your flare will be.

There are <b>two</b> ways to do this.

<b>First way</b>: 

    flares
    219,218,220,0.0,0.0,f,-1,0,0.50, default


The first node (<b>219</b>) is where the flare comes from and the other 2 (<b>218</b>, <b>220</b>) 
determine whether it faces front or back of the <b>plane</b>.

<a href="/images/flares-tutorial-pic1.jpg"><img src="/images/flares-tutorial-pic1.jpg">
    <br>The 1<sup>st</sup> image shows my plane nodes <b>0</b>, <b>1</b>, <b>217</b>, <b>218</b></a>
<a href="/images/flares-tutorial-pic2.jpg"><img src="/images/flares-tutorial-pic2.jpg">
    <br>The 2<sup>nd</sup> image shows the nodes where my flares are going to be placed 
        (optional to have them or not, just there to make things more precise and save time).</a>
<a href="/images/flares-tutorial-pic3.jpg"><img src="/images/flares-tutorial-pic3.jpg">
    <br>The 3<sup>rd</sup> image shows the placement for the left headlight, 
        the first node <b>219</b> is where the flare comes from and <b>217</b>, <b>218</b> 
        makes it face frontwards, if I did <b>218</b>, <b>217</b> the flare would face the other way.</a>
<a href="/images/flares-tutorial-pic4.jpg"><img src="/images/flares-tutorial-pic4.jpg">
    <br>The 4<sup>th</sup> image shows the placement for the right headlight, 
        the first node <b>220</b> is where the flare comes from 
        and <b>219</b>, <b>217</b> makes it face frontwards.</a>


To do the rest of the headlight flares, all I change is the first node, but keep the other two nodes depending on the side you want it. 
<hr>

The <b>other way</b> to do it is without the nodes where the headlights would be (you need to move the flare with the the red marked numbers).

    219,218,220,<font color=red>0.0</font>,<font color=red>0.0</font>,f,-1,0,0.50, default


All you would do it replace the first node, so instead of <b>219</b>, it would be <b>0</b> and then you would move the flare to the left.

    flares
    219,218,220,0.0,0.0,f,-1,0,0.50, default


    flares
    0,218,220,0.0,0.0,f,-1,0,0.50, default

Same thing apply for rear lights, top lights, side lights, just needs to have a plane, doesn't matter how big or how small the plane is since you can move the flare with the red marked numbers.
<hr>

# Syntax 

Borrowed from [[Truck Description File|Truck_Description_File]]: 

'''1: Reference Node''' '''2/3: X / Y'''<br>'''4/5: offsetX / offsetY'''<br>This defines where the light flares will be. It is positioned in relation to 3 nodes of the chassis. One node is the reference node, and the two others define a base (x,y). So the flare is in the plane defined by the 3 nodes, and is placed relative to the reference node by adding a fraction of the vectors ref-&gt;x and ref-&gt;y. The three first parameters are the 3 nodes numbers (ref,x,y) and the two next gives what amount of ref-&gt;x and ref-&gt;y to add to displace the flare point (these two should be logically between 0 and 1, or else that means you use the wrong base triangle and if the body flexes too much the flare will not stick to the body correctly). 

Basically, OffsetX/Y means that a fraction of X and Y will be added to the Reference node, which should be a corner, with a Y node above it, and an X node to the right or left of it. It's a bit easier, however, if it's in a left corner, than a right. 

Example (* = node, + = flare location): 

  *
    +
  *   *

Hint: Use the material name "tracks/aimflare" for help in positioning a flare.  

Alright, back on topic: below the syntax, you should begin listing your nodes, keeping in mind their location on the vehicle, and the coordinate plane. You'll probably need to save, open up RoR, and test out the flares quite a few times before the placement of the flare is perfect.

# Adding Symmetrical Flares  

Okay, so you finally have that headlight, taillight, marker light, whatever-light 
in place. Now, you need one for the opposite side. Never fear, however, because 
there's a quite simple way of figuring out how to exactly place the other side's flare. 
Remember above, when it was stated, "these two should be logically 
between 0 and 1" about offset-X and offset-Y? 

Well, anyway, once you have the first flare placed, just use that same exact placement line again, 
but this time, subtract whatever offset-X you used on the first flare from 1.0. 
Example: say we placed this headlight: 


    flares
    ;RefNode,X,Y,OffsetX,OffsetY, Type, ControlNumber, BlinkDelay, size MaterialName
    0,10,1,0.345,0.55,f


That'd be the left side. To get the right side, we'd have to take 0.345 and subtract it from 1.0 to get 0.655. Then, we use 0.655 for the right side's offset-X. Since we want the right side flare to be at the same height as the left side, we use the same offset-Y. So, in turn, it'd look like this: 


    flares
    ;RefNode,X,Y,OffsetX,OffsetY, Type, ControlNumber, BlinkDelay, size MaterialName
    0,10,1,0.345,0.55,f
    0,10,1,0.655,0.55,f


<br>This guide uses headlamps as an example, but this technique can be used to place any type of flare. 



# Troubleshooting Flares 

Should the flare seem to stick to the interior of the vehicle when you select REF, X and Y nodes from the left side of the chassis, just use three nodes&nbsp;directly opposite on the right side of the chassis&nbsp;instead.&nbsp; This should thereby make the flare stick to the outside of the vehicle. 

If you had to add nodes to a vehicle to place flares, and the flares seem to swing around or fall to the ground, ensure that you tied the said nodes into the&nbsp;frame of the vehicle&nbsp;with beams. 

If a flare isn't illuminating when you attempt to turn it on, verify that the syntax is correct; the flare line has the correct REF, X & Y nodes; that it is of the correct type; and that the control number (if it's a user-controlled light) is correct.  The flare could be showing up inside the vehicle, check the wireframe (hit K).  If this is the case, see above.


