Custom texture splatting
============


## Introduction

So, you want to make nice looking map with detailed textures? Here is the place ;-)

Alpha-splatting is a technique that allows you to place detailed tiled textures on your terrain. Their implementation follows RGBA (Red-Green-Blue-Alpha) images. With the files that are suggested here you can also apply an overlay map which means that you can vary the color of each of your detailed textures by blending a big image over them (the textured you used before alpha-splatting for example).

<div class="info-box">
<p class="title">Note: this article doesn't refer to our <a href="/technical/terrn2-subsystem.html">terrain system</a>. </p>
<p>Techniques here are relevant for old Terrn subsystem or advanced users who want to create meshed terrains.</p>
<p>Our terrain system currently doesn't allow making your own shaders, you need to use it's builtins.</p>
</div>

2 shaders are discussed here. Choose **<u>one</u>** of them:

### Shader 1

**PROS**

* Have an overlay texture
* Blend the textures nicely over each other

**CONS**

* Need for a shader file (\*.cg) and a program file (\*.program)
* Limited to 8 textures
* Sizes of the tiles are all the same
* The overlay texture always darken the terrain and lowers the contrast of the detailed textures

### Shader 2

**PROS**

* Only consists of a material file (simpler)
* Unlimited (or supposed so) number of detailed textures
* Tile size can be set for each texture individually
* The contrast and luminosity of your textures remain unaltered

**CONS**

* No overlay texture (if you want one)
* Slightly harsher transition between textures

## Shader 1

**Before starting** make sure you have the shader, program and material file from the following link: <http://www.ogre3d.org/tikiwiki/Terrain+Alpha+Splatting>.

Let's keep the things simple. We'll begin with only 3 detailed textures.

   1.   Make a RGB image defining your zones (eg: red for grass, green for sand, blue for rocks). Do it just as you did for the groundmodel. If you used RGB colors for your ground-model you can re-use this file.

!! DO NOT USE DDS TEXTURES FOR THOSE RGBA IMAGES !! They compress the image and give some pixels the average colors of their neighbors. Then those pixels that are not exactly red, green or blue will look black on your terrain in RoR, ruining your work...
    2.   Prepare your detailed textures and save them as dds - Paint.net is free and embeds the DDS exporter. Keep the resolution not too high (512\*512 is a good compromise today in 2010) otherwise your map will lag a lot.
    3.   Locate this line in the material file:

    param_named pageSize float 1024

This parameter (1024) should correspond to your heightmap (the \*raw) size - 1 (i.e. your heightmap is 513\*513 then this parameter should be 512\*512).

   4.   Locate this code in the material file:

    fragment_program_ref AlphaSplatTerrain/FP 
                                         { 
                                                  param_named alpha0Mask float4 1 1 1 0 
                                                  param_named alpha1Mask float4 0 0 0 0 
                                          }

These settings are OK for our use but it is useful to understand their meaning: each 1 activates an alpha-splatting channel. In this example we will only use the three first channels of our first RGBA image (so we'll use Red, Green and Blue channel. Not alpha because the fourth parameter is set to 0). If you want to use more channels then you have to activate them here.

    5.   Go to the end of file and locate the following code:

    material DemoSplatTerrainShader&nbsp;: AlphaSplatTerrain
        { 
            set_texture_alias AlphaMap1 alphamap1.png 
            set_texture_alias AlphaMap2 black.png 
            set_texture_alias Splat1 gras.jpg 
            set_texture_alias Splat2 moos2.jpg 
            set_texture_alias Splat3 schlamm_getrocknet1.jpg 
            set_texture_alias Splat4 gras.jpg 
            set_texture_alias Splat5 gras.jpg 
            set_texture_alias Splat6 moos2.jpg 
            set_texture_alias Splat7 schlamm_getrocknet1.jpg 
            set_texture_alias Splat8 gras.jpg 
            set_texture_alias Detail Detail3.jpg 
            set_texture_alias Fallback cooltex.jpg
          }

Here you have to reference the images you prepared before. AlphaMap1 is your RGB image. AlphaMap2 isn't used as you didn't activate the corresponding channels. Fill Splat 1,2,3 with the name of your detailed textures.

    6.   You just have to tune the terrain CFG file by enabling the vertexnormals (that will automatically shade your map) and adding the name of the material to use for alpha-splatting (so replace "DemoSplatTerrainShader" by your material name):

    ## The name of the material you will define to shade the terrain 
    CustomMaterialName=DemoSplatTerrainShader

Actually you just have to copy the one of the ogre example. The material name is defined just before referencing the images in the code (see the code above) and that's it!

If you don't rename anything then you don't have to alter program and shader (\*.cg) files at all.

## Shader 2

This shader was introduced in RoR first by Fat-Alfie. He kindly sent it to me as I needed an alpha-splat shader without the overlay texture.

### Pre-requisites

Take the code below and make a file containing it named : *yourmapname*-alphasplat.material (of course replace yourmapname with what you want). Place this file into your map folder.

*The extension "-alphasplat" is not mandatory but why not setting a guideline here? That will make our RoR-life easier.*

    material RoRwiki-alpha
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
                    // we use the gravel texture as the base, other textures are blended over it
                    texture gravel.dds
                    scale 0.007 0.007
                }
            }
            // detail texture 1 pass
            pass
            {
                lighting off
                // blend with former pass
                scene_blend alpha_blend
                // only overwrite fragments with the same depth
                depth_func equal
                // alpha map for the grass
                texture_unit
                {
                    texture mapname_alpha_1.png
                    // use alpha from this texture
                    alpha_op_ex source1 src_texture src_texture
                    // and colour from last pass
                    colour_op_ex source2 src_texture src_texture
                }
                // detail texture
                texture_unit
                {
                    texture grass.dds
                    scale 0.007 0.007
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

### Let's go

You can see in the shader that there 3 passes (base pass, detail texture 1 pass and lightning pass). Each pass correspond to a "layer" that Ogre (graphical engine) will add to your terrain. Each one is blended over the previous ones.

#### Giving your material a name

First replace "RoRwiki-alpha" with your material name (choose one, containing no spaces)

#### Base pass

This pass will tile a texture all over the map. All the other textures will be blended over it.

-   You will need a detailed texture
-   Reference your detailed texture (replace "gravel.dds" with the name of your detailed texture)
-   Set its scale. Leave it as it is (0.007 0.007), you will judge if that's looks OK once you have this material in-game.

#### Detail texture 1 pass

In this pass you will apply your first texture except the base one. You need to provide an "alpha-map" to indicate where the texture should show on your terrain (white parts) and where it shouldn't (transparent parts). It is an image that should have the same size as your heightmap - 1 (e.g. heightmap is 513\*513, alpha map should be 512\*512). The most common format is PNG.

*Tip: you can derive those maps from your ground models*

<u>*!! DO NOT USE DDS TEXTURES FOR THOSE RGBA IMAGES !! They compress the image and give some pixels the average colors of their neighbors. Then those pixels that are not exactly red, green or blue will look black on your terrain in RoR, ruining your work...*</u>

-   You will need an alpha-map
-   You will need a detailed texture
-   Reference your alpha-map (replace "mapname\_alpha\_1.png" with your alpha-map name
-   Reference your detailed texture (replace "grass.dds" with your detailed texture name)
-   Set the scale (leave it as it is now, 0.007 0.007)

#### Adding more textures

For adding a new texture with its alpha map, simply copy the **detail texture 1 pass** and paste it before the lightning pass. Repeat the steps described before and add as many as you want!

#### Lightning Pass

This defines how your terrain should be shaded. Leave this pass as it is for now.

#### Referencing your material in the terrain CFG file

You just have to tune the terrain CFG file by enabling the vertexnormals (that will automatically shade your map) and adding the name of the material to use for alpha-splatting (so replace "DemoSplatTerrainShader" by your material name):

    ## The name of the material you will define to shade the terrain
    CustomMaterialName=RoRwiki-alpha

#### Done

Now include everything in your terrain ZIP file (alpha maps, detailed textures, material file, CFG), fire up RoR and cross your fingers!

## Last advice

And now it only begins!

To have a nice looking and very personal ground, spend time making your different textures fit together. Try to split some of the layers too (i.e. generate 2-3 kind of rocks, 2-3 kind of grasses). Use L3DT ( [<http://www.bundysoft.com/L3DT/>](http://www.bundysoft.com/L3DT/) ) to generate those images for you based on the curves and slopes of your terrain and make custom climates for controlling that all.

And the most important: look at the real world ;-)

-- DeGa (2010)
