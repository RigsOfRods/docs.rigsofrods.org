---
layout: page
title:  "Aircraft handling"
categories: [gameplay]
---

<div class="toc" markdown="1">
  * TOC
  {:toc}
</div>

# How to use the autopilot
	
You can find the autopilot on top of your dashboard in a plane. Upon startup it looks like this:

<a href="/images/autopilot-start.jpg">
<img src="/images/autopilot-start.jpg" width="640" height="40">
</a>

The autopilot has different modes you can engage or disengage by
pressing the buttons. When you change a value, the change is
immediately applied to the current mode.

## Heading modes

<a href="/images/autopilot-heading.jpg" >
<img alt="Autopilot heading.jpg" src="/images/autopilot-heading.jpg" width="200" height="40" /></a>

<ul><li> <b>HDG</b> (Heading): set the airplane heading to the heading selected (in degree)
</li><li> <b>WLV</b> (Wing Leveler): set the wings horizontal. The airplane should roughly keep its current heading.
</li><li> <b>NAV</b> (Radio Navigation): engage when approaching a runway equipped with an ILS equipment (the red and white antennas). The airplane will first try to intercept the runway axis, then stay along it until you pass the runway edge.
</li></ul>

### Heading Listings

<p>This is a list of headings to use for ILS on included maps.
</p>
<ul><li>North St. Helens main runway - 240 degrees
</li><li>Aspen main runway - 190 degrees
</li></ul>

### Altitude modes

<p>

        <a href="/images/autopilot-alt.jpg" class="image">

        <img a src="/images/autopilot-alt.jpg" width="242" height="39" /></a>
</p>
<ul><li> <b>HOLD</b> (Hold altitude): set the altitude to the altitude selected (in feet). The the maximum vertical speed allowed to reach the altitude is selected by the <b>vert.speed</b> setting (in feet per minute, the sign of the selected vert speed is ignored). So this mode works better with a vert.speed different than 0!
</li><li> <b>V/S</b> (Vertical Speed): set the vertical speed (in feet per minute), without a target altitude. Positive value to climb, negative to descent.
</li><li> <b>NAV+V/S</b> (Vertical Radio Navigation): when both NAV and V/S are selected, the altitude is controlled by the ILS system. So when approaching a runway with <b>NAV</b>, engage <b>V/S</b> to make the plane descend to the runway.
</li></ul>

### Speed mode

<ul><li> <b>ATHR</b> (Auto-Throttles) set the speed of the airplane as selected in IAS (Indicated Air Speed, in knots).
</li></ul>

### other buttons

<ul><li> <b>GPWS</b> (Ground Proximity Warning System): when engaged, a recorded voice calls altitude and warns in case of dangerous maneuvers close to the ground.
</li><li> <b>BRKS</b> (Parking brakes)
</li></ul>

## Horizontal Navigation Indicator (HSI)

<div class="floatleft">

        <a href="/images/autopilot-hsi.jpg" class="image">
        <img  src="/images/autopilot-hsi.jpg" width="141" height="144" /></a></div>
        
        
<p>There is a simplified HSI (Horizontal Navigation Indicator) instrument
between the AOA (Angle of Approach) indicator and the engine gauges. 
It includes:
</p>
<ul><li><ul><li> a compass
</li><li> a heading bug (that runs along the heading selector)
</li><li> two position indicators: 
<ul><li> a vertical bar for horizontal deviation
</li><li> a horizontal bar for vertical deviation. 
</li></ul>
</li></ul>
</li></ul>
<p>They tell you how far you are from the optimal trajectory when you do an ILS approach. The optimal position is when both bars are at the center of the display.
</p>

## How to do a successful instruments approach with the ILS

<ol><li>ensure the approach you want to do is equipped with an ILS: 
<ul><li>check if there are red and white antennas at the end of the runway, at the side where you will touch down. Be sure the approach is clear of obstacles. 
</li></ul>
</li><li>fly to a comfortable distance from the runway, preferably off the terrain. 
</li><li>ensure you are at the right altitude for an approach from that distance. If the horizontal bar is low, descend, if it is high, climb. 
</li><li>fly in a way so you will soon intercept the runway axis, or are roughly on the runway axis 
</li><li>Engage NAV, then V/S. Drop the joystick. The plane should fly by itself now, intercepting the runway axis and descending to the runway. 
<ul><li>You can see how it performs on the HSI display. The bars should cross at the center when the approach is stabilized. 
</li></ul>
</li><li>Control your speed! You should fly as slow as possible (around 100 knots for the Antonov 12). Use auto-throttle if possible. Watch the AOA, if it gets too high, you will stall! Add more flaps in that case. 
</li><li>If you go too fast, the plane will not descend and the horizontal bar will go down. 
</li><li>On short final, the GPWS calls "Minimums": you reached the minimum decision altitude. If you see the runway and everything is fine, proceed to the landing (real pilots disconnect the autopilot at this stage and land by the hand). 
</li><li>The autopilot should disconnect at the runway edge, but in some case it can continue to function, so be cautious at the flare. 
</li><li>Engage reverses and brake (press and maintain key B). You landed!
</li></ol>



