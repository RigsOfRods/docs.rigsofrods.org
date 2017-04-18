---
layout: page
title:  "Blender for beginners"
categories: [tools-tutorials]
---

<div class="toc" markdown="1">
  * TOC
  {:toc}
</div>


# Introduction

  <p>This tutorial is designed to provide a simple introduction to blender. This will not be covering any advance topics, it's sole purpose is to provide a small amount of knowledge that you can use to proverbially get your foot in the door of using blender. I am not going to cover how to install blender as i going to assume you are capable of doing that by yourself.</p>
  <p>This tutorial is designed for Blender 2.65a
     It may work with newer or older variants, i don't know what the future holds or when you are reading this. So a small word of warning; If you are using blender 25.45b then you are probably looking at something that is outdated.
  </p>


# Useful links

  <p><a rel="nofollow" class="external text" href="http://www.blender.org/">Blender homepage</a></p>
  <p><a rel="nofollow" class="external text" href="http://www.blender.org/download/get-blender/">Download Blender</a></p>
  <p><a rel="nofollow" class="external text" href="http://en.wikibooks.org/wiki/Blender_3D:_Noob_to_Pro#Table_of_Contents">A different Blender tutorial</a> (This goes into much more depth and may be harder to understand, but covers almost everything you could ever want to know)</p>

    
# This is Blender

 <div class="thumb tleft">
    <div class="thumbinner" style="width:602px;">
       <a href="/images/blender-beginner-01-splash.png" class="image">
       <img alt="" src="/images/blender-beginner-01-splash.png" width="600" height="375" class="thumbimage" /></a>  
       <div class="thumbcaption">This is what you should see</div>
   </div>
 </div>
 <p>This is the first thing you should see when you load up blender.</p>
 <div style="background-color:#FFFFCC; border: 1px solid #FFCC00; padding:0.2em; margin:1em 5em">
    <div style="float:left;"><a href="/images/WarningIcon.png" class="image"><img alt="WarningIcon.png" src="/images/WarningIcon.png" width="32" height="32" /></a></div>
    <div style="margin-left:40px"><strong>Warning</strong><br /> Do not panic, Its not all that bad. I promise</div>
 </div>
 <p><br />
    The first thing that i want you to do is click on the grey area that is covered in a grid, This should remove the big box in front of you.
 </p>
 <div class="thumb tleft">
    <div class="thumbinner" style="width:602px;">
       <a href="/images/blender-beginner-02-start.png" class="image">
       <img alt="" src="/images/blender-beginner-02-start.png" width="600" height="375" class="thumbimage"   /></a>  
       <div class="thumbcaption">This is what you will be working with
       </div>
    </div>
 </div>

 <p>So first things first, you should now be looking at a grey box. It doesn't look like much yet but believe me it will be a work of art once you have finished with it <s>[/sarcasm]</s></p>
 <p>Currently you are in object mode, this is indicated by the box with object mode written on it at the bottom of the viewing window (the bit your cube is displayed in)
    You can select objects by right clicking on them, such as the cube. When you right click on something you will see an orange border around it, this indicates it is the object that is currently selected. 
    There is a little diagram at the bottom left of the viewing window which you can look at if you forget or can not tell which way you are looking. The arrows point into the positives of each axis (as opposed to the negative/minus numbers)
 </p>
 <div style="padding: .2em .3em; margin: .2em .2em; background-color: #c1ffc1; border: solid 1px #a0ffa0; font-size: 92%;">
    <b>Note:</b> 
    <p>You can rotate your view by holding down your mouse wheel and moving your mouse. </p>
    <p>You can pan around by holding down shift + your mouse wheel and moving your mouse</p>
    You can also scroll by scrolling up and down on your mouse wheel
 </div>
 <p>That is the basics of navigating your object.</p>
 <p>You can move your cube along thee different axis. These are red, blue and green. If you click and hold on one of the arrows you can move the object in that direction around your screen, you can also right click and hold anywhere when you have a selected item to drag it around your screen, but i advise that you stick to using the three arrows as it is much easier to use because it is much easier to gauge where you are actually moving the object.
    There are three arrows that have a colour individual to each one:
 </p>
 <p>Blue = z axis</p>
 <p>Green = Y axis</p>
 <p>Red = X axis</p>
 <div class="thumb tleft">
    <div class="thumbinner" style="width:602px;">
       <a href="/images/blender-beginner-03-editmode.png" class="image">
       <img alt="" src="/images/blender-beginner-03-editmode.png" class="thumbimage"  /></a>  
       <div class="thumbcaption">
         Changing to edit mode
       </div>
    </div>
 </div>
 <p><br /></p>
 <p>To modify your cube you will need to switch to edit mode. This is because in object mode you can modify objects (individual 3d models) , whereas in edit mode you can edit the object itself.</p>
 <p>To do this:</p>
 <p>Make sure you have your cube selected with an orange glow around it, remember this is done by right clicking the cube. Then once you have done that you have to go to the bar at the bottom of the viewing window and click where it says "object mode" a list will then pop up. From that list select "edit mode" and you will then be in edit mode.</p>
 <div style="padding: .2em .3em; margin: .2em .2em; background-color: #c1ffc1; border: solid 1px #a0ffa0; font-size: 92%;">
    <b>Note:</b> Which mode to use?
    <p>Object Mode is Moving or adjusting objects models</p>
    Edit Mode is Changing the actual model
 </div>
 <p>If you have done this correctly then your cube should now be tinted orange, this is because by default all of the faces (sides), edges (lines) and vertices (angles/joints) have been selected. This is also similar to when you selected the object earlier. if you haven't already noticed the theme, anything that has been selected will be orange in some way or form.</p>

# Editing your cube

 <div class="thumb tleft">
    <div class="thumbinner" style="width:602px;">
       <a href="/images/blender-beginner-0-editmode.png" class="image">
       <img alt="" src="/images/blender-beginner-04-editmode.png" width="600" height="375"  /></a>  
       <div class="thumbcaption">
         You've made it into edit mode, this is where the work actually begins&#160;:D
       </div>
    </div>
 </div>
 <p>Now that you are in edit mode it is time to edit your cube.</p>
 <p>First you may notice that your object is a little low on polygons, currently you have a grand total of 6 polygons and nothing awesome was ever created with just 6 polygons. So to fix this we need to move our cursor to the left hand pane of the screen labelled "mesh tools". In this pane there are several functions that you can use to modify your model, The options shown will depend on which mode you currently have blender in (remember edit and object mode). We are going to use the tool called subdivide, all you have to do is click it and you will find your cube now has 24 polygons. Now to be completely honest with you that is still quite low, but for now it will do.</p>
 <div style="padding: .2em .3em; margin: .2em .2em; background-color: #c1ffc1; border: solid 1px #a0ffa0; font-size: 92%;"><b>Note:</b>  It is always best to try and make sure you keep all of your faces 4 sided, if you don't subdividing may cause you issues. This doesn't mean you cant use 3 sided faces if you have to but try and keep them to a minimum.</div>
 <p>Now that you have subdivided your cube it is time to make it into something. For the purpose of this tutorial we are going to make a house (essentially a 3d pentagon)</p>
 <div class="thumb tleft">
    <div class="thumbinner" style="width:602px;">
       <a href="/images/blender-beginner-house1.png" class="image">
       <img alt="" src="/images/blender-beginner-house1.png" width="600" height="375" class="thumbimage"  /></a>  
       <div class="thumbcaption">
          Select these 3 vertices
       </div>
    </div>
 </div>

 <p><br />
    So the first part of turning this run of the mill cube into a house is to select the three top central vertices (points/angles etc... From now on i am only going to refer to these as vertices) you can do this by holding shift while right clicking on them. Once again note how they have turned Orange, have a guess why?
 </p>
 <p>The vertices may appear to have moved very slightly when you selected them, don't worry about this. It is one of the quirks of the program/ your pc screen/ your eyes that you will have to get used to.</p>
 <p>Now you are going to use the blue (z axis) and drag the vertices up into a roof like shape, you will now see that the house is taking shape and although it may look like the roof has triangles in it you will find that it does not (which is good).</p>
 <div class="thumb tleft">
    <div class="thumbinner" style="width:602px;">
       <a href="/images/blender-beginner-house2.png" class="image">
       <img alt="" src="/images/blender-beginner-house2.png" width="600" height="375" class="thumbimage"  /></a>  
       <div class="thumbcaption">Best house evar!!1!1!!!!1!!!
       </div>
    </div>
 </div>

 <p>You will now have something that looks vaguely reminiscent of this house shaped model. It doesn't have to be identical, as long as you are doing the same things you are learning the same things.</p>
 <p>But believe it or not most 3d house models are slightly more complex than this, so more work may be needed. Unless you are creating models for a scene where you never get more than 100 meters within said model if that is the case then job well done, get yourself a cup of tea and a well deserved chocolate digestive.</p>

# More detail

  <p>In this section we are going to add more detail to the building, please note that while more detail makes something look nicer it can also decrease the in game fps. So when you create a "to scale 1:1 replica of the uss enterprise" be warned that it may lag a little in blender its self, never mind rigs of rods or whatever else you wish to add this into.</p>
  <div class="thumb tleft">
     <div class="thumbinner" style="width:602px;">
        <a href="/images/blender-beginner-detail1.png" class="image">
        <img alt="" src="/images/blender-beginner-detail1.png" width="600" height="375" class="thumbimage"  /></a>  
        <div class="thumbcaption">
          The polygon count is over 9000! (well, 96 is close enough)
        </div>
     </div>
  </div>
  <p>We will want to subdivide the object again (go back up if you have forgotten how).</p>
  <p>Once you have done that we will add a bay window to your house.</p>
  <div class="thumb tleft">
     <div class="thumbinner" style="width:602px;">
        <a href="/images/blender-beginner-bay-window1.png" class="image">
        <img alt="" src="/images/blender-beginner-bay-window1.png" width="600" height="375" class="thumbimage"  /></a>  
        <div class="thumbcaption">
           Select these vertices
        </div>
     </div>
  </div>

  <p>To do this we are going to move the highlighted vertices in the image to the left </p>
  <p>First you should highlight said vertices (shift+right click). Then you are going to use the red arrow to drag them outwards, this will make the house shape much more appealing.</p>
  <div class="thumb tleft">
     <div class="thumbinner" style="width:602px;">
        <a href="/images/blender-beginner-door1.png" class="image">
        <img alt="" src="/images/blender-beginner-door1.png" width="600" height="375" class="thumbimage"  /></a>  
        <div class="thumbcaption">
          Next we are going to add a door, well it kind of looks like one
        </div>
     </div>
  </div>

  <p>Now we are going to make something that kind of looks like a door. I wouldn't worry to much as to what it looks like as long as you are learning the techniques that's all that matters for now.</p>
  <p>First we are going to select these six vertices, these are where the edges of the door will be, then we are going to use the extrude region tool (its just above subdivide) when you click on that you will then be able to move that area backwards and forwards. I would suggest that you indent it slightly so it looks a bit like a door.</p>
  <div class="thumb tleft">
     <div class="thumbinner" style="width:602px;">
        <a href="/images/blender-beginner-door2.png" class="image">
        <img alt="" src="/images/blender-beginner-door2.png" width="600" height="375" class="thumbimage"  /></a>  
        <div class="thumbcaption">Notice the lip at the bottom of the door, it is evil
        </div>
     </div>
  </div>

  <p><br />
     Notice the lip at the bottom of the door, while it is fine to have it there in blender, it may cause issues when you put it into a game such as rigs of rods. This is because in most 3d game engines faces (side of model/object) only have 1 side, this means you can only see the face from 1 side. On a 3d model this inst an issue because you have multiple faces meaning the backface (side of face that cant be seen) is hidden by other faces. But in the case of this 2d lip it will not be. In rigs of rods if you do this on the collision mesh then you may experience collision issues with the building if a car crashes into the door. 
  </p>
  <p>So lets delete it, blender offers a multitude of delete options which are all useful for different things</p>
  <p>In this case we want to delete the edge which will in turn delete the face which will get rid of the problem. So first you need to select the two vertices of the lip, the two that need selecting are the ones at each end of the lip. Then you need to press the delete key on your keyboard. This will bring up a menu with several options.</p>
  <p>You do not want to delete the vertices because this will also delete a lot of the rest of the model.</p>
  <p>You do not want to delete the face because there is no face selected</p>
  <p>You also do not want to delete all of the above or any combination of them</p>
  <p>All you want to delete is the the edge. so you click on that. Next time you try and delete something it will put the mouse cursor over the edge option for you, this is to try and allow you to work faster if you are trying to delete multiple similar things in a repetitive style.</p>

  <h1><span class="editsection">[<a href="/rorwikibackup/index.php?title=Blender_mesh_tutorial&amp;action=edit&amp;section=6" title="Edit section: Texturing (UV mapping)">edit</a>]</span> <span class="mw-headline" id="Texturing_.28UV_mapping.29"><font size="6">Texturing (UV mapping)</font></span></h1>
  <p>For this i am going to keep it simple so we are ditching the house. You may want to save it first.</p>
  <div style="background-color:#FFFFCC; border: 1px solid #FFCC00; padding:0.2em; margin:1em 5em">
     <div style="float:left;"><a href="/images/WarningIcon.png" class="image"><img alt="WarningIcon.png" src="/images/WarningIcon.png" width="32" height="32" /></a></div>
     <div style="margin-left:40px"><strong>Warning</strong><br />Always keep backups of files, you have no ideas how many times i have seen great projects die because of this. This also doesn't just apply to rigs of rods, this applies to everything in life.
        A good method if you have the space is to create a main folder for the whole project, then for each save you make you create a new folder inside that one named after the time and date the file was saved. This means you have lots of backups should anything go wrong
     </div>
  </div>
  <p><br /></p>
  <p>For this section of the tutorial we are going to use a plain old cube, mainly because it only has 6 sides making it easy to work with.</p>
  <div class="thumb tleft">
     <div class="thumbinner" style="width:602px;">
        <a href="/images/blender-beginner-cube.png" class="image">
        <img alt="" src="/images/blender-beginner-cube.png" width="600" height="375" class="thumbimage"  /></a>  
        <div class="thumbcaption">
           This is some next gen cry-engine graphical awesomeness we have here
        </div>
     </div>
  </div>
  <p>So you are back at square one, this is a cube. Please make sure it has 6 faces and 8 vertices , if it doesn't then you have already done something wrong (for the intent of this tutorial). </p>
  <div class="thumb tleft">
     <div class="thumbinner" style="width:602px;">
        <a href="/images/blender-beginner-edge-select.png" class="image">
        <img alt="" src="/images/blender-beginner-edge-select.png" width="600" height="358" class="thumbimage"  /></a>  
        <div class="thumbcaption">
           There always has to be one indie screen shot
        </div>
     </div>
  </div>
    
  <p>First switch into edit mode (you can use "tab" if your a hotkey ninja) Then select the button that is on the bar at the bottom of the viewing window that has a cube with a line on it. When you highlight over it you will see a message saying edge select. If you still cant find it just look to the right of where it says "global"</p>
  <div class="thumb tleft">
     <div class="thumbinner" style="width:602px;">
        <a href="/images/blender-beginner-mark-seams.png" class="image">
        <img alt="" src="/images/blender-beginner-mark-seams.png" width="600" height="375" class="thumbimage"  /></a>  
        <div class="thumbcaption">
           Think back to making a net of something in school
        </div>
     </div>
  </div>

  <p>Now you have to mark the edges. To do this you need to select the edges of your model that will allow you to unwrap it as 1 whole layer. Similar to if you are peeling an orange in 1 continuous layer (i cant be the only one who tries to do that?)
     So all you have to do is hold down ctrl while clicking the edges you wish to select. You want the seems to unfold to make a T shape.
  </p>

 
   <p><strong>**WORK IN PROGRESS - The rest of the tutorial is glued from an older one, for blender 2.49 or previous.**</strong></p>

  <p>Skins in Rigs of Rods are made by draping the beams in triangles known as submeshes.  Textures are cut up and placed by coordinate and percentage.  This is <i>a lot</i> of work by hand, and luckily Blender does it all for you.</p>
  
  <h2><span class="editsection">[<a href="/rorwikibackup/index.php?title=Blender_Tutorial_3&amp;action=edit&amp;section=1" title="Edit section: Applying Texture">edit</a>]</span> <span class="mw-headline" id="Applying_Texture">Applying Texture</span></h2>
  <p>Enter <a href="/rorwikibackup/index.php/File:Objectmode.png" class="image"><img alt="Objectmode.png" src="/rorwikibackup/images/6/66/Objectmode.png" width="132" height="25" /></a> and select your truck.  Press <tt>f</tt> to enter <i>UV Face Select</i>.  Enter UV/Image Editor by clicking the <i>Windows Type</i> button, see on the right.  Click <tt>Image &gt; Open Image</tt> and select your trucks texture.  Because there is no real texture for the tutorial truck, just pick any image.  I am using a picture of my cat, because I can.</p>
  <p><br />
     Select triangles by right clicking them, holding <tt>SHIFT</tt> to select multiple triangles.  You can now adjust the texture placement.  In the UV/Image Editor, use left click to adjust the position of the triangle on the texture.  Right click a corner of the triangle and use the left click to adjust its position.  This may be time consuming and may require some trial-and-error.  Take your time, because you're almost done!
  </p>
  <p>
         <a href="/images/blender-beginner-old-uv.png" class="image">
         <img alt="/images/blender-beginner-old-uv.png" width="800" height="600" /></a></p>
  <p>From here, make a <a href="/rorwikibackup/index.php/Material_File" title="Material File">Material File</a> for your truck and set it in your globals... export your truck, and you're done!</p>
  <p><br />
     <b>EDIT: in blender 2.46 there isn't a "UV face edit", go to edit mode and press "U"</b>
  </p>
  <h2><span class="editsection">[<a href="/rorwikibackup/index.php?title=Blender_Tutorial_3&amp;action=edit&amp;section=2" title="Edit section: Exporting in Blender">edit</a>]</span> <span class="mw-headline" id="Exporting_in_Blender">Exporting in Blender</span></h2>
  <p>You must export to an alreading existing truck file. Blender will NOT make the truck file for your when you hit 'Export'.</p>
  <p>Make sure the truck file you're exporting to has the word 'submesh' right above the word 'end'.</p>
  <p><br />
     Now, when in Blender, go into object mode.
  </p>
  <p>Right-click on the submesh so there is a pink outline around it and you shouldnt see very many beams if you are actually clicked on the submesh. and in the left hand bottom corner make sure it says submesh after ME and OB (there might be some letters and numbers befor the word submesh. this is ok)</p>
  <p>Also if you try to export and it says "wings section not found, unable to export wings"  just click on the boxes in the bottom left had corner that say OB:(some stuff here) ME:(some stuff here and rename it submesh on BOTH ME and OB and it will now work.</p>
  <p>After that if you have the blender ror importer and exporter installed.( witch im sure you do if you got the car into blender in the first place) click file-export-RoR exporter, then find the truck file you are exporting to and click export.</p>
  <p>Blender should just pause for a second and then return to normal activity. and when you go to your truck file you should see all the submesh stuff in the truck file. </p>
  <p>Also Blender will automatically make a copy of your original truck  file from befor you exported it. open that using notepad and copy the node and beem sections into your new truck file that has the submesh because blender will have messed those up. but by doing that it will put it back to normal.</p>




