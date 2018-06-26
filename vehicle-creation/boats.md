---
title: "Boats"
layout: page
categories: [vehicle-creation]
---

<div class="toc" markdown="1">
  * TOC
  {:toc}
</div>

# Making a buoyant hull

Step1: What you have to do is make a simple boat hull shape out of nodes. 
You can make many different shaped hulls, they will affect the performance of the boat.
Try your best to use the least amount of nodes as possible, 
For a typical hull, you should use from 10-30 nodes at the most. 
 
Step2: When you finish your softbody, you need to [submesh](/technical/fileformat-truck#submesh) it. 
Submeshing it will allow the boat to float, instead of sinking.
 
Step3: try it out ingame. It should float nicely. 
If it sinks, then there is a hole in the hull of the boat. 
Once you find your mistake, it will float.
 
# Adding an engine, i.e. "screwprop"
 
Step1: To create a chassis, or setup for the screwprop, 
you must have 3 nodes in a triangular shape
and stabalizing it with beams,
  
The picture illustrates the setup. Please imagine the box is actually a boat-hull :)
 
![](/images/nautical-screwprop.png) 
  
Step2: You should enter the "screwprops" section into your .boat file.

then, you can have your own sea exploration! :-)

```
screwprops
;    prop node, back node, top node,  power
             3,         1,         2, 100000.0
``` 
