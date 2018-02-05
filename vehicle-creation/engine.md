---
title: "Engine"
layout: page
categories: [vehicle-creation]
---

<div class="toc" markdown="1">
  * TOC
  {:toc}
</div>

# Engine (land vehicles)



 The engine sections are used for vehicles which are driven through their wheels (trucks). Together, they specify the type of engine being used (truck or car), the power of that engine and the gear ratios for the truck 
 <table id="toc" class="toc">
    <tr>
       <td>
          <div id="toctitle">
             <h2>Contents</h2>
          </div>
          <ul>
             <li class="toclevel-1 tocsection-1">
                <a href="#Engine"><span class="tocnumber">1</span> <span class="toctext">Engine</span></a>
                <ul>
                   <li class="toclevel-2 tocsection-2">
                      <a href="#Settings"><span class="tocnumber">1.1</span> <span class="toctext">Settings</span></a>
                      <ul>
                         <li class="toclevel-3 tocsection-3"><a href="#Torque"><span class="tocnumber">1.1.1</span> <span class="toctext">Torque</span></a></li>
                         <li class="toclevel-3 tocsection-4"><a href="#Differential_ratio"><span class="tocnumber">1.1.2</span> <span class="toctext">Differential ratio</span></a></li>
                         <li class="toclevel-3 tocsection-5"><a href="#Gear_ratios"><span class="tocnumber">1.1.3</span> <span class="toctext">Gear ratios</span></a></li>
                      </ul>
                   </li>
                   <li class="toclevel-2 tocsection-6"><a href="#More_Information"><span class="tocnumber">1.2</span> <span class="toctext">More Information</span></a></li>
                </ul>
             </li>
             <li class="toclevel-1 tocsection-7">
                <a href="#Engoption"><span class="tocnumber">2</span> <span class="toctext">Engoption</span></a>
                <ul>
                   <li class="toclevel-2 tocsection-8">
                      <a href="#Settings_2"><span class="tocnumber">2.1</span> <span class="toctext">Settings</span></a>
                      <ul>
                         <li class="toclevel-3 tocsection-9"><a href="#Engine_Inertia"><span class="tocnumber">2.1.1</span> <span class="toctext">Engine Inertia</span></a></li>
                         <li class="toclevel-3 tocsection-10"><a href="#Engine_Type"><span class="tocnumber">2.1.2</span> <span class="toctext">Engine Type</span></a></li>
                      </ul>
                   </li>
                </ul>
             </li>
             <li class="toclevel-1 tocsection-11"><a href="#Torque_Curve"><span class="tocnumber">3</span> <span class="toctext">Torque Curve</span></a></li>
          </ul>
       </td>
    </tr>
 </table>
 <h1> <span class="mw-headline" id="Engine"> Engine </span></h1>
 <p>This section specifies torque, gearing and RPM ranges of the engine being used. </p>
 <h2> <span class="mw-headline" id="Settings"> Settings  </span></h2>
 <p>See <a href="http://docs.rigsofrods.org/vehicle-creation/fileformat-truck/#engine" title="Truck Description File">Truck_Description_File#Engine</a> for reference manual.</p>
 <h4> <span class="mw-headline" id="Torque"> Torque  </span></h4>
 <p>Tuning torque in RoR is a tricky topic, since the current air resistance simulation is overstrong. Setting torque to provide realistic acceleration at low speeds results in severely stunted top speeds. Setting it to provide higher top speeds results in very strong acceleration. </p>
 <p>Engine Inertia also has a <b>VERY</b> important role in engine behavior since this value also determines how fast a vehicle can accelerate </p>
 <h4> ratio <span class="mw-headline" id="Differential_ratio"> Differential ratio  </span></h4>
 <p>Differential ratio represents gear reduction ratio between input pinion gear and the ring gear of the differential. This parameter acts as global gear conversion ratio. It means that if, let's say first gear has ratio 13.86 and differential ratio is 2.0, actual first gear reduction is 27.72 (2.0 * 13.86). If you are using real gearbox parameters, bear this in mind and look for real differential ratios too.<br /> </p>
 <h4> <span class="mw-headline" id="Gear_ratios"> Gear ratios<br />  </span></h4>
 <p>Gear ratios of forward gears. For every turn of the wheel must engine turn this many times (not counting the differential ratio). When setting various gear ratios, try to make smaller difference between higher gears. Pleas note that in sample gear setting the difference (ratio) between first and second gear is approx. 45&#160;%, but difference between the fifth and sixth gear is about 19&#160;%. This allows smoother gearbox performance. There must be between 3 and 15 forward gears. <b>The last gear must be followed by a -1 value.</b><br /></p>
 <h2> <span class="mw-headline" id="More_Information"> More Information </span></h2>
 <p>A great source of practical gear ratios is from <a rel="nofollow" class="external text" href="http://www.roadranger.com/Roadranger/productssolutions/transmissions/index.htm">Eaton Fuller</a>. To see the ratios, click the name of the transmission and find <b>Product Specifications Guide</b>. If your vehicle decelerates in a gear you may not have enough power, or too high a gear. NOTE: the value of this site is unknown. RoR's poor air resistance simulation probably invalidates the use of any real life gear ratios: It's always best to make sure a truck can sensibly use all the gears it has. </p>
 <p>If you know a little about vehicles there is a <a rel="nofollow" class="external text" href="http://www.grimmjeeper.com/gears.html">Gear Ratio Guide</a>, but a a decent knowledge of transmissions, transfer cases, underdrives and correct rear end gears is highly recommended. </p>
 <h1> <span class="mw-headline" id="Engoption"> Engoption </span></h1>
 <p>This optional section allows the user to specify whether the engine is for a car or heavy truck and the engine inertia of the vehicle. </p>
 <h2> <span class="mw-headline" id="Settings_2"> Settings  </span></h2>
 <p>See <a href="http://docs.rigsofrods.org/vehicle-creation/fileformat-truck/#engoption" title="Truck Description File">Truck_Description_File#Engoption</a> for reference manual.</p>
 <h4> Inertia <span class="mw-headline" id="Engine_Inertia"> Engine Inertia  </span></h4>
 <p>The default game value is 10.0, which is correct for a large diesel engine, Use higher values to make engines accelerate more slowly and stall more difficultly, which may be useful for vehicles towing large masses. This value should be lowered for smaller, light engines (Is the multiplier different for car and truck engines?) </p>
 <p>With a high value of inertia the engines RPM is not likely to change when resistance is met. As an example, when changing gears a high inertia will cause the wheels to slip, while a lower value will cause the engine RPM to change and prevent the wheels from slipping. However, with a low inertia and a high brake value, the engine will stall more easily since the brakes can change the RPMs more easily. </p>
 <p>If your engine doesn't change its RPM's during gear change, your engine inertia is too high </p>
 <p>If a vehicle is feeling sluggish, and hard to brake, it is better to decrease the inertia than increase the brake force, and torque.<br /> </p>
 <h4> Type <span class="mw-headline" id="Engine_Type"> Engine Type  </span></h4>
 <p>Using (c) for cars or (t) for trucks specifies characteristics of the engines. Car engines use a different sound to truck engines and have no turbocharger. They also have less inertia by default. (t) is the default.</p>
 <h1> <span class="mw-headline" id="Torque_Curve"> Torque Curve </span></h1>
 <p>This section allows you to define a torque curve for your vehicle. It is optional.</p>
 <p>This allows you to assign predefined torque curves or your own custom curves to a truck. Predefined options are: default, diesel, turbodiesel, gas, turbogas, wheelloader, compacttractor, tractor, hydrostatic </p>
 <p>Predefined Curve Example<pre>
    torquecurve
    turbogas
    </pre> 
 </p>
 <p>The first number is RPM where the power begins, and the second defines power as a percent of total torque. </p>
 <p>It's suitable to define the torque to the engine RPM set in the engine definition plus 25% ( multiply the value with 1.25) to get the overev area defined. </p>
 <p>The following example would be good for a maximum engine RPM set to 2800.<br /> </p>
 <p>Custom curve example<pre>
    torquecurve
    0,0
    1000,0.79
    1500,0.9
    2000,0.97
    2500,0.99
    3000,0.9
    3500,0.77
    </pre> 
 </p>
 <p>Engine dying in idle and first gear&#160;? Just define a single higher peak value where you want the engine to idle...&#160; like adding: </p> 
 <pre>
    ...
    700, 0.2
    800, 0.6
    900, 0.4
    ...

 </pre> 
 <div class="thumb tleft">
    <div class="thumbinner" style="width:121px;">
       <a href="/images/truckfile-torquecurve.png" class="image">
       <img alt="a torque curve example" src="/images/truckfile-torquecurve.png" width="119" height="27"  /></a>  
       <div class="thumbcaption">
          
          Example
       </div>
    </div>
 </div>
 to the example above in the right spot will result the engine idle a little bit higher then 800 rpm in first gear. 
 <p>The example to the left shows a screenshot of a torquercurve made for a small diesel engine: </p>
 <p>Idle: ~600 RpM, Max @ 1900 RPM, slight and constant torque increase over the used RpM bandwidth, hard torque dropoff in the overev area. </p>

