---
layout: page
title:  "Ogre legacy materials"
categories: [technical]
---

<div class="toc" markdown="1">
  * TOC
  {:toc}
</div>

[pic1-white-ball]: /images/ogre-old-materials-01.jpg
{: width="100%"}
[pic2]: /images/ogre-old-materials-02.jpg
{: width="100%"}
[pic3-diff-tex]: /images/ogre-old-materials-03-diff-tex.jpg
{: width="100%"}

[pic4]: /images/ogre-old-materials-04.jpg
{: width="100%"}
[pic5]: /images/ogre-old-materials-05-spec-tex.jpg
{: width="100%"}
[pic6]: /images/ogre-old-materials-06-norm-text.jpg
{: width="100%"}
[pic7]: /images/ogre-old-materials-07-ball.jpg
{: width="100%"}
[pic8-silo-red]: /images/ogre-old-materials-08-silo-red.jpg
{: width="100%"}
[pic9-silo-green]: /images/ogre-old-materials-09-silo-green.jpg
{: width="100%"}
[pic10-silo-blue]: /images/ogre-old-materials-10-silo-blue.jpg
{: width="100%"}
[pic11]: /images/ogre-old-materials-11-metal.jpg
{: width="100%"}
[pic12]: /images/ogre-old-materials-12-metal.jpg
{: width="100%"}
[pic13]: /images/ogre-old-materials-13-silo.jpg
{: width="100%"}

[[Image:Materials-pic1.jpg|thumb|right|250px|Pic 1 - 3D ball without material assignment in Blender (render)]]
[[Image:Materials-pic2.jpg|thumb|right|150px|Pic 2 - Object without material assignment in RoR]]
[[Image:Materials-pic3.jpg|thumb|right|250px|Pic 3 - Tennis ball diffuse texture]]
[[Image:Materials-pic4.jpg|thumb|right|250px|Pic 4 - Tennis ball 3D with diffuse texture only (render Blender)]]
[[Image:Materials-pic5.jpg|thumb|right|250px|Pic 5 - Tennis ball specular texture]]
[[Image:Materials-pic6.jpg|thumb|right|250px|Pic 6 - Tennis ball normal map texture]]
[[Image:Materials-pic7.jpg|thumb|right|250px|Pic 7 - Tennis ball 3D with diffuse, specular and normal textures (render blender)]]

# What is a material?

At the beginning of everything is a mesh. Note that a terrain is itself some kind of mesh too.

Let's say you modeled a ball in a 3D program (<u>pic 1</u> - Blender in this example). 
It's now a bare ball, showing with a default colour. In the picture, I use Blender, so it appears whitish.
In RoR, when an object has no material it appears white (<u>pic 2</u>).
Now let's say you want to make your ball look like a tennis ball. 
For making it realistic, you will need to consider a lot of details, for example:

* A diffuse texture. For a tennis ball, example shown in <u>pic 3</u>. 
  It basically defines the colour to be used. The result in 3D with 
  only the diffuse texture is shown in <u>pic 4</u>
* A specular texture. For a tennis ball, example shown in <u>pic 5</u>. 
  It defines which parts are shiny, and which one are not. 
  The green "fur" should not be shiny at all while the white stripes should be.
* A Normal map. For a tennis ball, example shown in <u>pic 6</u>. The result in 3D is shown on <u>pic 7</u>.

The material will contain all the settings to apply those textures and effects 
to your mesh in Rigs of Rods. This is a configuration file, 
where you specify all the parameters for making everything like you want.

They can be very simple (just a non-reflective plain colour) 
or quite complex (normal shading, alpha-splatting).

**Note that if you need some advanced techniques, you will need a "custom shader". 
This part is not covered here, just know that those shaders contains 
new algorithms to produce new advanced effects.**

# Tutorial

## Get a silo mesh

TODO: fix old link: http://www.rigsofrods.com/attachment.php?attachmentid=196679&d=1303428882

When you export a mesh from your 3D program and convert it to a *.mesh object, this object only contains the name of the material(s) it will use. 
It means that with a simple text file on the side, you can make it pink, transparent, shiny or whatever you like!
Nevertheless, you cannot change the name of the material assigned to your mesh, so pay attention when naming them in your 3D program.
You can find attached a map. It is necessary for showing the mesh without bothering you with map edition. Install it like any other map mod. 

When you load the map, the silo looks terrible plain white. It is because the material file is empty, and the material is not correctly defined.
See <u>pic 1</u>
![pic1-white-ball]

## "Hello world": write your first material by yourself! Give it a plain colour

If you look inside the map zip, you will find two interesting files, neglect the rest:
silo.mesh: This is the 3D model of the ball, with no material
silo.material: This is the material 
If you open the material file, you'll see nothing. Copy the following code in it (which mean: extract this file from the zip, edit it with a text editor, save it and repack it into the map zip, overwriting the previous one):

    material silo
    {
    	technique
    	{
    		pass
    		{
    			ambient 1.000000 0.000000 0.000000 1.000000
    		}
    	}
    }

The first line declares a material with its name. The name of the material file (*.material) does not have any importance.

The second line is the technique - don't touch, it is about deep modification of the material. 
It mainly "talks" to the graphic card. It's about light and shadows.

Then on the third line, there is a pass. For a simple material, you need just one pass. 
The interesting parameters for us are defined inside the pass.

**Note: For more complex material, you can add several pass each one after the other.
That way you can ask the graphic engine to apply different "layers" of effects 
(example: The first pass defines a diffuse texture, the second pass adds normal-mapping).**

Load the map, there is a strange reddish cucumber, like in <u>pic 8</u>, that's it! 
OK, you've managed to get your first simple material working.

## Play with ambient, diffuse and specularity 

In the file, you can see only one line "ambient" followed by some values.

    material silo
    {
    	technique
    	{
    		pass
    		{
    			ambient 1.000000 0.000000 0.000000 1.000000
    		}
    	}
    }

The 3 first values are RGB (red-green-blue) values for diffuse map (diffuse map defines the colour of the material). 
You can see those values are set to 1 1 0
It means that our object will appear red when lighted by ambient light. Ambient light is the light that does not come directly from the sun (or other light source).
In the <u>pic 8</u>, you can see the silo of our example looking red.

![pic8-silo-red] Caption: Pic 8 - Silo with red ambient

Nevertheless, it looks full white where lightened by the sun directly.

Add a line in the material file, that it looks like the following one:

    material silo
    {
    	technique
    	{
    		pass
    		{
    			ambient 1.000000 0.000000 0.000000 1.000000
    			diffuse 0.000000 1.000000 0.000000 1.000000
    		}
    	}
    }

By adding that line, you specify that the parts that are directly lightened by the sun should show green.
See the result in <u>pic 9</u>.

![pic9-silo-green]  caption: Pic 9 - Silo with red ambient and green diffuse

Our material is not perfectly plain, it is a bit reflective too. 
For specifying the colour and the intensity of the light that is reflected, 
add another line to the material, it now should look like this:

    material silo
    {
    	technique
    	{
    		pass
    		{
    			ambient 1.000000 0.000000 0.000000 1.000000
    			diffuse 0.000000 1.000000 0.000000 1.000000
    			specular 0.000000 0.000000 1.000000 1.000000 12.500000
    		}
    	}
    }

Now the parts hit perpendicularly by the sun reflect a blue light.
See result in <u>pic 10</u>.

![pic10-silo-blue]  caption: Pic 10 - Silo with red ambient, green diffuse and blue specular

For nice results, you will need to adjust the intensity of each source. 
Most often the colour is not changed much, but the intensity is set different for each section.

## Add a texture to it

Now we want to add a metal plate texture to our silo. For that, you should have "unwrapped" your 3D model before. 
It means telling the model where to apply which part of the texture. 
If you have correctly defined this, the texture unit will automatically get those coordinates and look in RoR as it does in your 3D program.

For that, let's add a new section inside the pass, which will be a texture unit. 
Reference metalPlates.jpg, that image is already contained in the zip

    material silo
    {
    	receive_shadows on
    	technique
    	{
    		pass
    		{
    			ambient 0.500000 0.500000 0.500000 1.000000
    			diffuse 0.640000 0.640000 0.640000 1.000000
    			specular 0.500000 0.500000 0.500000 1.000000 12.500000
    			texture_unit
    			{
    				texture metalPlates.jpg
    			}
    		}
    	}
    }

When you try it in game, you should see something like in <u>pic 11</u>.

![pic11] Caption: Pic 11 - Silo with metal plates tiled texture bad

Il looks bad, it's far too much reflective, too dark when not directly exposed to the sun and the texture should be tiled more (being smaller).
For correcting this, we'll modify the material as follows:

    material silo
    {
    	receive_shadows on
    	technique
    	{
    		pass
    		{
    			ambient 0.600000 0.600000 0.600000 1.000000
    			diffuse 0.640000 0.640000 0.640000 1.000000
    			specular 0.100000 0.100000 0.100000 1.000000 12.500000
    			texture_unit
    			{
    				texture metalPlates.jpg
    				scale 0.3 0.3
    			}
    		}
    	}
    }

Parameters of ambient, diffuse and specular have been tuned and the scale of the texture adjusted.
You should have a silo looking like the one in <u>pic 12</u>, which looks better.

![pic12] caption: Pic 12 - Silo with metal plates tiled texture better

## Advanced multi-pass material for combining leaks with metal plates tiles texture (alpha-splatting)

![pic13] image caption: Pic 13 - Silo with metal plates tiled and leaks

See <u>pic 13</u> for an example of what some advanced shader can do by combining multiple textures. 
This same material is also used for terrain alpha-splatting.

A line begining by // means that it is commented.

    material silo
    {
        receive_shadows on
        technique
        {
            // base pass
            pass
            {
                lighting off
                texture_unit
                {
                    // we use the metal plates texture as the base, other textures are blended over it
                    texture metalPlates.jpg
                    scale 0.3 0.3
                }
            }
            // leaks pass
            pass
            {
                lighting off
                // blend with former pass
                scene_blend alpha_blend
                // only overwrite fragments with the same depth
                depth_func equal
                // alpha map for the leaks
                texture_unit
                {
                    texture leak.png
                    // use alpha from this texture
                    alpha_op_ex source1 src_texture src_texture
                    // and colour from last pass
                    colour_op_ex source2 src_texture src_texture
                }
                // detail texture
                texture_unit
                {
                    texture leak.png
    				// the scale is set to 1:1 because we don't want this texture to be tiled
                    scale 1 1
                    // alpha blend colour with colour from last pass
                    colour_op_ex blend_diffuse_alpha src_texture src_current
                }
            }
            // lighting pass
            pass
            {
                ambient 1 1 1
                diffuse 1 1 1 
                depth_func equal
                scene_blend zero src_colour
            }
        }
    }

# Further information ==

Links to exhaustive Ogre documentation:

http://www.ogre3d.org/tikiwiki/Materials

http://www.ogre3d.org/docs/manual/manual_14.html#SEC23

