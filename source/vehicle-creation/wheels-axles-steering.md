Wheels, axles, steering
============



## Wheels


 wheels are simply structures that the game creates automatically out of standard features to make creating vehicles easier. They are simply [nodes](/vehicle-creation/fileformat-truck#nodes) connected by [beams](/vehicle-creation/fileformat-truck#beams) with a contactable [submesh](/vehicle-creation/fileformat-truck#submesh). They are unique in that they will rotate when given input to accelerate.
 
[Wheels](/vehicle-creation/fileformat-truck#wheels) are the most basic wheels in the game. The width of a wheel is determined by the distance between the two reference nodes and is composed of pie slices known as rays. The more rays a wheel has, the smoother it will be but will also contain more nodes and beams and consequently lower performance. It is considered good form to keep your rays between 10 and 20. 
 <p>
    <a href="/images/wheels-pic1.png" class="image">
    <img alt="Wheelspic1.png" src="/images/wheels-pic1.png" width="500" height="500" /></a>
 </p>
The optional snode option allows for game-managed [Axle Rigidity](#axle-rigidity). This will keep the two wheel reference nodes in line under normal conditions. If snode is NOT used, you must enter 9999.
 <div class="thumb tnone">
    <div class="thumbinner" style="width:502px;">
       <a href="/images/wheels-pic2.png" class="image">
       <img alt="" src="/images/wheels-pic2.png" width="500" height="150" class="thumbimage" /></a>  
       <div class="thumbcaption">Nodes 2 and 3 would be mounted to the chassis with wheels mounted on nodes 1,2 and 3,4</div>
    </div>
 </div>
 
<pre>wheels
;radius, width, numrays, node1, node2, snode, braked, propulsed, arm, mass,  spring,   damping,   facemat          bandmat
0.54,   1,  12,       1,     2,   9999,    1,      1,         25,  400.0, 800000.0, 4000.0, tracks/wheelface tracks/wheelband2
0.54,   1,  12,       3,     4,   9999,    1,      1,         23,  400.0, 800000.0, 4000.0, tracks/wheelface tracks/wheelband2
</pre>
 
 <p>First step: The snode is Disabled ( The data is 9999), the nodes 1 and 4 are hanging just down. </p>

 <pre>wheels
 ;radius, width, numrays, node1, node2, snode, braked, propulsed, arm, mass,  spring,   damping,   facemat          bandmat
 0.54,   1,  12,       1,     2,      3,    1,      1,         25,  400.0, 800000.0, 4000.0, tracks/wheelface tracks/wheelband2
0.54,   1,  12,       3,     4,   9999,    1,      1,         23,  400.0, 800000.0, 4000.0, tracks/wheelface tracks/wheelband2
</pre>
 
 Second step: You type 3 to the snode option of the wheel 1,2. Now node 1 will always have the ambition to be at the same "line" like the nodes 2 and 3. </p>

 <pre>wheels
;radius, width, numrays, node1, node2, snode, braked, propulsed, arm, mass,  spring,   damping,   facemat          bandmat
0.54,   1,  12,       1,     2,      3,    1,      1,         25,  400.0, 800000.0, 4000.0, tracks/wheelface tracks/wheelband2
0.54,   1,  12,       3,     4,      2,    1,      1,         23,  400.0, 800000.0, 4000.0, tracks/wheelface tracks/wheelband2
</pre>

 Third step: You type 2 to the snode option of the wheel 3,4. 
 
 Now all nodes will be on one level / line even node 1 and 4 aren't mounted primary to the chassis.
 
## Wheels2
 
 <p>This feature improves the default wheels section by splitting wheels into rims and tires. This allows the player to set tire pressure with the keyboard.  </p>
[Wheels2](/vehicle-creation/fileformat-truck#wheels2) (also known as the "complex wheel model") allows you to separate the wheel [rim] from the tire (tyre). This requires extra syntax, namely specifying the characteristics of the wheel versus the tire. Traditionally the wheel will be very rigid with the tire being much less so. The rigidity of wheels2 tires can be altered by holding [ and ] ingame, resulting in this:
 <table style="margin: 1em auto;" class="wikitable">
    <tr>
       <td> Inflated tire</td>
       <td> Deflated tire</td>
    </tr>
    <tr>
       <td> <a href="/images/wheels2-screenshot-inflated.jpg" class="image">
          <img alt="Screenshot 3.jpg" src="/images/wheels2-screenshot-inflated.jpg" width="189" height="189" /></a>
       </td>
       <td> <a href="/images/wheels2-screenshot-deflated.jpg" class="image">
          <img alt="Screenshot 4.jpg" src="/images/wheels2-screenshot-deflated.jpg" width="174" height="174" /></a>
       </td>
    </tr>
 </table>
 <p>The adjustable tire pressure allows you to adjust handling in real-time. Lower pressure creates more grip while higher pressure creates more stability. </p>


## Meshwheels 


[Meshwheels](/vehicle-creation/fileformat-truck#meshwheels) takes advantage of a mesh's static nature. It also creates a smoother tire. The wheel rim is a standard Ogre3D mesh.
 <p>Meshwheels are very similar to normal wheels, but require specification of the wheel rim radius. Likewise, the direction the wheel is facing must be specified in order for the mesh to be rotated properly.<sup>1</sup> </p>
 <table style="margin: 1em auto;" class="wikitable">
    <tr>
       <td> Here is an example picture of a rim mesh, as it should be modeled. The actual tire will be added dynamically and will still flex.</td>
       <td> This material should be slightly different to other tire materials as it covers both the tire face and the tire wall:</td>
    </tr>
    <tr>
       <td> 
          <a href="/images/wheels-meshrim.jpg" class="image">
          <img alt="Meshrim.jpg" src="/images/wheels-meshrim.jpg" width="193" height="203" /></a>
       </td>
       <td> 
          <a href="/images/wheels-tire-texture.jpg" class="image">
          <img  src="/images/wheels-tire-texture.jpg" width="256" height="64" /></a>
       </td>
    </tr>
 </table>

### Notes 


The mesh should be centered (Where should the wheel be placed in the L/R direction? Should it face left or right?) and of the right size for the wheel you want to do: its outer diameter should be as the `rim_radius` parameter, and its width should be the same as the distance between `node1` and `node2`. </li>
	
All wheels are able to do skid steering. See the [steering](https://archives.rigsofrods.org/wiki/index.php/RoRBook/Steering) chapter.

It is considered good form to keep your rays between 10 and 20.

## Axles 

 <p>This section defines axles on a vehicle, allowing more accurate distribution of torque among the wheels. </p>

Sample axle section:

```
axles
w1(1 2), w2(3 4), d(ol) ; axle 1
w1(5 6), w2(7 8), d(l) ; axle 2

```

 <p>The axle section introduces open differentials, and Spooled (aka locked) differentials. By adding axles to your vehicle file you override the propulsed property for the tires. Only wheels connected to an axle are powered, if multiple axles are defined the axles are interconnected in a locked manner. If no axle section is defined the old model of equal power distribution is used. Because the axle sections looks up already defined wheels, it must be defined <b>AFTER</b> the wheels have been defined</p>
 <p>The axle section if different from other sections in that it is broken into properties, properties are not order dependent, currently the available properties are: </p>
 <ul>
    <li><b>w1(&lt;node1&gt; &lt;node2&gt;)</b> - this defines which wheel the axle is attached to, &lt;node1&gt; and &lt;node2&gt; refer to the node1 and node2 as defined in the wheel section </li>
    <li><b>w2(&lt;node1&gt; &lt;node2&gt;)</b> - wheel 2, same as w1, this is the second wheel attached to the axle. w1 and w2 are interchangeable.</li>
    <li>
       <b>d(&lt;list of diff types&gt;)</b> - Defines the available differential types for this axle. the list of axles is cycled through in the order specified, differential types maybe specified more than once. Each differential type is specified by a single letter, the letters are not to be separated by spaces or any other character. if no differentials are specified  the axles will default to opened and locked. 
       <ul>
          <li>
             <b>Available differential types</b>
             <ul>
                <li> <b>o</b> - open</li>
                <li> <b>l</b> - locked</li>
                <li> <b>s</b> - Split evenly (each wheel gets equal torque regardless of wheel speed)</li>
             </ul>
          </li>
       </ul>
    </li>
 </ul>

### Problems?

 <p>Wheel weight has a big effect on top speed since heavy wheels have lots of rolling resistance in RoR. Try to make the wheels as light as possible. If the wheels explode, they probably have too high damping for the weight. If the wheels and rpm needle start shaking, set lower clutch torque in the engoption section. This can take some tweaking, but it's worth it.</p>
 <p>Used together with fusedrag and realistic truck weight, real torque is often enough so there's no need to have several thousand hp engines. That makes the trucks easier to drive and better handling.</p>
 <p><br /></p>


## Axle Rigidity
   

See Also: [Suspension](/vehicle-creation/suspension)

 The <strong class="selflink">Axle Rigidity</strong> keeps the wheel aligned with the axle of the vehicle. It is used to avoid having to make a complex structure in order to hold the wheel in place. In fact, it keeps the two wheel nodes and the defined node in a straight line. This is intended to use with solid non-steerable axles. However, you probably can devise a way to use this as independent suspension.
 <p>Normally a wheel needs some sort of pyramidal hub to support it, such as the image to the right.  Axle rigidity allows you to avoid making this by doing some internal magic to keep the nodes supported.  Wheels need at least 2 nodes to define their width, and the node used for axle rigidity is the innermost node of the wheel.</p>
 <p>
    <a href="/images/wheels-axle-rigidity.jpg" class="image">
    <img alt="Rigidaxle2.jpg" src="/images/wheels-axle-rigidity.jpg" width="400" height="300" /></a>
 </p>
 <p>Here, the black beam are normal beams.  Red beams are a crude suspension set up.  Light-blue nodes are the outermost wheel nodes, while green nodes are axle rigidity nodes.</p>
 <p>For the left wheel (defined by nodes 1 and 2), the special rigidity node will be 3, and for the right wheel (defined by nodes 3 and 4), the special rigidity node will be 2.</p>


## Reference Arm Node 

 <p>This is to help modders, as I have seen a few asking about what this does.</p>

### What it does 

 <p>The reference arm node in the .truck file serves an important purpose. That purpose is to determine where the torque reaction in a chassis will be. If that node is placed in front of the specified wheel, then it will provide more traction, as the wheel pushes the chassis down into the ground. This is good for vehicles such as off-roaders and high-grip racecars. If the arm node is behind the specified wheel, then grip will be reduced as the wheel will help lift the chassis off the ground. This is useful for drifters and other cars and trucks that need less grip.</p>

### How it is Implemented

 The arm node is implemented through the [wheels](/vehicle-creation/fileformat-truck#wheels) section of a `.truck` file.

### Example Vehicle

 A good example vehicle that shows how the arm node works is box5diesel's [Baja Trophy Truck](http://archives.rigsofrods.net/repo/files/repofiles-2nd-batch/BajaTrophyTruck.zip). When in the air, if you accelerate in 6th gear, the nose of the truck will be lifted up. If you brake while in the air, the nose of the truck will be pushed down.  This is due to the arm nodes of the rear wheels being located in front of the rear axle, and the arm nodes for the front wheels, located behind the front axle.

### Example Diagram 

 <p>This is a rough diagram I made to show how it works. 
    In the top diagram, the arm node is behind the wheel, so as the wheel spins counterclockwise, it applies upward force to the node(red) in the blue circle, therefore imparting <i><b>less</b></i> traction as the chassis is pushed <i><b>upward</b></i>.In the bottom diagram, the arm node is in front of the wheel, so as the wheel spins counterclockwise, it applies downward force to the circled node, therefore imparting <i><b>more</b></i> traction as the chassis is pushed <i><b>downward</b></i>.
 </p>

![arm-node](/images/wheels-reference-arm-node.jpg)


## Steering

 Steering is made possible with the use of [hydros](/vehicle-creation/fileformat-truck#hydros). A proven steering set up which involves a diamond wheel support and a small chassis which the suspension is attached to. When this concept is realized, steering is not too difficult. 

### Wheel Mount

 <p>This is a typical wheel support diamond ("face octahedron"). This will carry the wheel independently from the main chassis. For example: </p>
 <p>
        <a href="/images/wheels-steering-octahedron.png" class="image">
        <img alt="Oktraeder.png" src="/images/wheels-steering-octahedron.png" width="427" height="483" /></a> 
</p>

The "wheel" nodes labeled here will become the position for the [wheels](/vehicle-creation/fileformat-truck#wheels). The distance between the two nodes will determine the wheel width. It is wise to make the diamond symmetrical for stability (that is, the height equals the width). You will need one of these for every wheel that is steerable.

If you find your nodes are contacting the ground and obstructing movement, you can make specific nodes non-contactable. See the [nodes](/vehicle-creation/fileformat-truck#nodes) syntax.
 
![wheelhub-wheel](/images/wheels-steering-wheelhub.jpg)
 
### Axle

 <p>The axle is actually simply built out of four beams: </p>
 <p>
        <a href="/images/wheels-steering-axle.png" class="image">
        <img alt="Achse.png" src="/images/wheels-steering-axle.png" width="333" height="282" /></a> </p>
        
 <p>But you need a rocker, too. However it's easy to build. This only requires two nodes in front of the axle (be aware these nodes should be at least 80cm from the axle away) and beams attached to them as shown at this picture: </p>
 <p><a href="/images/wheels-steering-schwinge.png" class="image">
 <img alt="Schwinge.png" src="/images/wheels-steering-schwinge.png" width="540" height="402" /></a></p>

### Hydros 

After the steering chassis is completed, the hydros](/vehicle-creation/fileformat-truck#hydros) can be added. Hydros are simply beams that change length when you press the right and left arrow keys, and are typically used for steering (although you can use them for other purposes if you so wanted).

 <p>In order to define a hydro, some specific information is needed. </p>
 <ol>
    <li>Node 1 - One end of the hydro </li>
    <li>Node 2 - The other end of the hydro </li>
    <li>
       Factor - The decimal percentage (0.2 = 20%) representing how far a hydro can extend. 
       <ol>
          <li>The length of a hydro can be determined by <tt>Original Length ± (Original Length * Factor)</tt></li>
       </ol>
    </li>
 </ol>
 <p>A hydro can also have two optional parameters: </p>
 <ol>
    <li><i>i</i> - The Hydro will be invisible </li>
    <li><i>s</i> - At approximately 20km/h to 40km/h the factor will be lowered gradually to 0 and will then be disabled. This is commonly used for rear-wheel turning, as it is disabled at high speed.</li>
 </ol>

Example Syntax:
 
      hydros
      ;node1, node2, factor, options</dt>
      43,    37,    -0.2,   i
      46,    36,     0.2,   s

 <p>The following example shows how hydros will push and pull nodes in a direction to induce steering: </p>
 <p>
        <a href="/images/wheels-steering-hydros.png" class="image">
        <img alt="Hydros.png" src="/images/wheels-steering-hydros.png" width="482" height="353" /></a> </p>


## Finished Steering Axle

The finished axle can look like this:

![finished-axle](/images/wheels-steering-complete.png)

Don't forget to add suspension (as covered in the previous chapter)


## Braked Steering  
 
 It is possible to have a steering system that only turns one side of wheels. In the [wheels](/vehicle-creation/fileformat-truck#wheels) section, set the `Wheel Braking` value to 2 or 3 for left or right wheel respectively. This works well for emulating tracked vehicles such as bulldozers. These usually do not work well at high speed.





