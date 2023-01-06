# nodeSnap

## Introduction

  <p>nodeSnap is a new open source truck editor heavily inspired by the old rorEditorizer.</p>
  <p>This tutorial will show you how to use and manipulate nodeSnap (version 0.1.1-beta)</p>

## Get started

   <p>You can download nodeSnap from the repository following <a rel="nofollow" class="external text" href="https://forum.rigsofrods.org/resources/nodesnap-truckfile-editor.775/">this link.</a></p>
   <p>The current version is a stand-alone app (which means, it doesn't require an installer) so you will find it in a zip format.</p>
   <p>You might ask: But why is it ~67MB while rorEditorizer is ~729KB?</p>
   <small>nodeSnap is built using new technologies, such as Electron and node.js. That might be overkill for this application, but that's how it became possible in the first place. Next versions will make that size worth it with much more features.</small>

   <div class="thumb tleft">
      <div class="thumbinner" style="width:602px;">
         <a href="/images/nodeSnap-1.jpg" class="image">
         <img alt="" src="/images/nodeSnap-1.jpg" class="thumbimage" /></a>  
      </div>
   </div>
   <p>After downloading the zip file, you can put it anywhere you want. I moved it to my desktop.</p>

   <div class="thumb tleft">
      <div class="thumbinner" style="width:602px;">
         <a href="/images/nodeSnap-2.jpg" class="image">
         <img alt="" src="/images/nodeSnap-2.jpg" class="thumbimage" /></a>  
      </div>
   </div>
   <p>Extract it to a <b>folder</b> (important)</p>

   <div class="thumb tleft">
      <div class="thumbinner" style="width:602px;">
         <a href="/images/nodeSnap-3.jpg" class="image">
         <img alt="" src="/images/nodeSnap-3.jpg" class="thumbimage" /></a>  
      </div>
   </div>
   <p>Then double click on "nodeSnap" to run it.</p>
   <div class="thumb tleft">
      <div class="thumbinner" style="width:602px;">
         <a href="/images/nodeSnap-24.jpg" class="image">
         <img alt="" src="/images/nodeSnap-24.jpg" class="thumbimage" /></a>  
      </div>
   </div>

## Create a new truck file

   <p>To create a new truck file, all you have to do is to click on "New File" under "Actions" and fill up the form, then click on "Next".</p>

## Open a truck file

   <p>To open a truck file, simply click on "Open file" under "Actions" and navigate to your desired truck file.</p> 
   <small><b>Note:</b> nodeSnap supports all of RoR's truck file extensions.</small>

## Interface

   <div class="thumb tleft">
      <div class="thumbinner" style="width:602px;">
         <a href="/images/nodeSnap-4.jpg" class="image">
         <img alt="" src="/images/nodeSnap-4.jpg" class="thumbimage" /></a>  
      </div>
   </div>
   <p>nodeSnap's UI looks like rorEditorizer. On the left side, we have a sidebar that shows you all the nodes and beams with their details and on the top, we have a toolbar that contains functions.</p>
   <p>In the middle, we have 4 views: Top, Side, Front, and 3D. The first three views are orthographic and the last one is a perspective view. In the middle of the views, you have a selector that you can drag to resize the views. On each view, you have a 'viewCube' (3ds max inspired) that can help you get to certain angles easily. (currently works only on the 3D view)</p>

   <div class="thumb tleft">
      <div class="thumbinner" style="width:602px;">
         <a href="/images/nodeSnap-5.jpg" class="image">
         <img alt="" src="/images/nodeSnap-5.jpg" class="thumbimage" /></a>  
      </div>
   </div>
   <p>On the sidebar, click on the "Other" tab, click on "Settings" button to access the current editor's settings. These settings allow you to change the grid size (it affects node snapping), to change a visual node's size and to toggle node names.</p>
   <small><b>Note:</b> These settings are saved as preferences for each truck file you make/edit in a ".nodeSnap" folder that you can find in the root truck file's directory.</small>

## Controls

   <h4>Camera:</h4>
   <ul>
      <li>Right click + mouse move => move camera around</li>
      <li>
            Left click + mouse move (Only on perspective view aka 3D view)
            => rotate on axis
      </li>
      <li>Mouse wheel => Zoom</li>
   </ul>
   <h4>Editor:</h4>
   <ul>
      <li>CTRL + N => truck mode (default)</li>
      <li>CTRL + B => blueprint mode</li>
      <br />
      <li>
            Truck Mode:
            <ul>
               <li>Mouse double left click => new node</li>
               <li>
                  Mouse double left click + CTRL => new node snapped on
                  grid
               </li>
               <li>Mouse click on a node + drag => Move node around</li>
               <li>
                  Mouse click on a node + drag + CTRL => Move node around
                  with grid snapping to the preset value
               </li>
               <li>
                  CTRL + SHIFT + click node1 + click node2 => Creates a
                  beam + shows a temporary blue line before you click on
                  the second node
               </li>
            </ul>
      </li>
      <br />
      <li>
            Blueprint Mode:
            <ul>
               <li>Mouse + gizmo => transform</li>
               <li>Key "S" => scale mode</li>
               <li>Key "R" => rotate mode</li>
               <li>Key "T" => translate mode</li>
            </ul>
      </li>
   </ul>

## Functions

   <div class="thumb tleft">
      <div class="thumbinner" style="width:602px;">
         <a href="/images/nodeSnap-6.jpg" class="image">
         <img alt="" src="/images/nodeSnap-6.jpg" class="thumbimage" /></a>  
      </div>
   </div>
   <p>nodeSnap includes a few useful functions to make your editing experience easier.</p>
   <p>We will use this simple structure as an example.</p>
   <small>A structure is an N/B, either the whole N/B or an N/B inside of a group.</small>

   <div class="thumb tleft">
      <div class="thumbinner" style="width:602px;">
         <a href="/images/nodeSnap-19.jpg" class="image">
         <img alt="" src="/images/nodeSnap-19.jpg" class="thumbimage" /></a>  
      </div>
   </div>
   <p>You can right click on a node in one of the views for a menu</p>

### Grouping

   <p>nodeSnap supports RoR's grouping and adds a few more functions to that. To add a new group, right click on a node, a window will ask you to name that group, and after clicking apply, nodeSnap will add that group affecting that node and all nodes after it.</p> 
   <div class="thumb tleft">
      <div class="thumbinner" style="width:602px;">
         <a href="/images/nodeSnap-7.jpg" class="image">
         <img alt="" src="/images/nodeSnap-7.jpg" class="thumbimage" /></a>  
      </div>
   </div>
   <div class="thumb tleft">
      <div class="thumbinner" style="width:602px;">
         <a href="/images/nodeSnap-9.jpg" class="image">
         <img alt="" src="/images/nodeSnap-9.jpg" class="thumbimage" /></a>  
      </div>
   </div>
   <div class="thumb tleft">
      <div class="thumbinner" style="width:602px;">
         <a href="/images/nodeSnap-8.jpg" class="image">
         <img alt="" src="/images/nodeSnap-8.jpg" class="thumbimage" /></a>  
      </div>
   </div>

   <p>After you add a new group, nodeSnap will offer you a few functions when you right click on the group.</p>
   <div class="thumb tleft">
      <div class="thumbinner" style="width:602px;">
         <a href="/images/nodeSnap-10.jpg" class="image">
         <img alt="" src="/images/nodeSnap-10.jpg" class="thumbimage" /></a>  
      </div>
   </div>
   <p>The functions are self explanatory.</p>

#### Duplicate a group

   <p>Instead of remaking the exact same structure somewhere else, nodeSnap offers a function to duplicate the current structure in a group and place it anywhere else you want.</p>

   <div class="thumb tleft">
      <div class="thumbinner" style="width:602px;">
         <a href="/images/nodeSnap-11.jpg" class="image">
         <img alt="" src="/images/nodeSnap-11.jpg" class="thumbimage" /></a>  
      </div>
   </div>
   <div class="thumb tleft">
      <div class="thumbinner" style="width:602px;">
         <a href="/images/nodeSnap-11.jpg" class="image">
         <img alt="" src="/images/nodeSnap-13.jpg" class="thumbimage" /></a>  
      </div>
   </div>
   <p>nodeSnap allows you to do an offset on the specified axis.</p>
   <small>All you have to do is to specify the offset (in RoR's one unit of distance) and how many times you want to duplicate the structure</small>

   <div class="thumb tleft">
      <div class="thumbinner" style="width:602px;">
         <a href="/images/nodeSnap-12.jpg" class="image">
         <img alt="" src="/images/nodeSnap-12.jpg" class="thumbimage" /></a>  
      </div>
   </div>
   <div class="thumb tleft">
      <div class="thumbinner" style="width:602px;">
         <a href="/images/nodeSnap-14.jpg" class="image">
         <img alt="" src="/images/nodeSnap-14.jpg" class="thumbimage" /></a>  
      </div>
   </div>
   <p>nodeSnap also allows you to do a mirror on the specified axis.</p>

   <div class="thumb tleft">
      <div class="thumbinner" style="width:602px;">
         <a href="/images/nodeSnap-15.jpg" class="image">
         <img alt="" src="/images/nodeSnap-15.jpg" class="thumbimage" /></a>  
      </div>
   </div>
   <small><b>Note:</b> You do not have to care about overlapped nodes after duplication, because nodeSnap takes care of that automatically.</small><br /><br />
   <small><b>Note 2:</b> nodeSnap does not copy beams that are connected between any node inside the group and an other node outside the group, keep reading for the solution.</small>

### Toolbar

   <p>On the toolbar, we have two drop down menus: "Edit" and "File"</p>

#### Edit menu

   <div class="thumb tleft">
      <div class="thumbinner" style="width:602px;">
         <a href="/images/nodeSnap-18.jpg" class="image">
         <img alt="" src="/images/nodeSnap-18.jpg" class="thumbimage" /></a>  
      </div>
   </div>
   <p>The edit menu has a few interesting functions. The "Scale" function gives you the ability to scale the whole n/b. The "Move" functions moves the whole n/b by an offset on a specified axis. The "Rotate" function rotates the whole n/b on a specified axis with a given angle in degrees.</p>
   <p>The "Duplicate Visible" function solves one problem you have when duplicating groups. Instead of duplicating a specific group, all you have to do is to hide all the nodes/groups that you do not want to duplicate, and execute the function, just like duplicating a group.</p>

#### File menu

   <div class="thumb tleft">
      <div class="thumbinner" style="width:602px;">
         <a href="/images/nodeSnap-17.jpg" class="image">
         <img alt="" src="/images/nodeSnap-17.jpg" class="thumbimage" /></a>  
      </div>
   </div>
   <p>The functions are pretty much self explanatory.</p>
   <small><b>Note:</b> nodeSnap has an integrated file watcher. This means that whenever you edit your truck file using a text-editor, nodeSnap will automatically reload the file.</small><br />
   <small><b>Note 2:</b> nodeSnap has a backup system. Each time you save your file, nodeSnap will make a backup of the previous truckfile and store it inside the ".nodeSnap" folder that is found in the root truck file's directory, ordered by a timestamp.</small><br />
   <small><b>Note 3:</b> nodeSnap is based on a "project" system, which means, if you leave the editor and go back to the project page, your work will not be lost and you will have an option to go back to your work. (this is integrated for future features)</small>

### Blueprint system

   <p>Like any 3D editor, you can load a blueprint in nodeSnap by going to the sidebar, clicking on the "Other" tab, and clicking on the "Load Blueprint"</p>
   <small><b>Note:</b> nodeSnap saves your blueprint data as preference and loads it again whenever you load the truck file again.</small>
   <div class="thumb tleft">
      <div class="thumbinner" style="width:602px;">
         <a href="/images/nodeSnap-20.jpg" class="image">
         <img alt="" src="/images/nodeSnap-20.jpg" class="thumbimage" /></a>  
      </div>
   </div>

#### Image

   <p>On the "Image" tab, select your file and press "Add"</p>
   <div class="thumb tleft">
      <div class="thumbinner" style="width:602px;">
         <a href="/images/nodeSnap-21.jpg" class="image">
         <img alt="" src="/images/nodeSnap-21.jpg" class="thumbimage" /></a>  
      </div>
   </div>
   <p>You can switch to blueprint mode (CTRL+B) and reposition, scale or rotate the blueprint by pressing (T, S, R) keys respectively.</p>
   <div class="thumb tleft">
      <div class="thumbinner" style="width:602px;">
         <a href="/images/nodeSnap-22.jpg" class="image">
         <img alt="" src="/images/nodeSnap-22.jpg" class="thumbimage" /></a>  
      </div>
   </div>
   <div class="thumb tleft">
      <div class="thumbinner" style="width:602px;">
         <a href="/images/nodeSnap-23.jpg" class="image">
         <img alt="" src="/images/nodeSnap-23.jpg" class="thumbimage" /></a>  
      </div>
   </div>
   <p>And then go back to truck editor mode using (CTRL+N)</p>

#### 3D Model

   <p>On the "3D Model" tab, select your file and press "Add"</p>
   <p>Again, you can switch to blueprint mode (CTRL+B) and reposition, scale or rotate the model by pressing (T, S, R) keys respectively.</p>
   <small><b>Note:</b> nodeSnap supports only ogre's XML files (".mesh.xml") or Wavefront object file (".obj")</small>

## Conclusion

   <p>nodeSnap is made to make editing N/Bs an easy task that anyone can do.</p>
   <p>For feature requests or bug reporting, please click <a rel="nofollow" class="external text" href="https://github.com/Max98/project_nodeSnap/issues">this link</a></p>
