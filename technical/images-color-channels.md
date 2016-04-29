---
layout: page
title:  "Images and color channels"
categories: [technical]
---

In daily computer usage, image files store photos and imagery. They can be produced by digital cameras, scanners and authoring tools, and viewed in image viewers.

In Rigs of Rods and 3d games in general, images are used for many various purposes besides plain display, they often display weird in image viewers and it's unclear how they were produced. This tutorial aims to explain it.

# Color chanels

An image file consists of 4 independent color channels, each storing intensity value on scale 0.0 (none) to 1.0 (full):

[channels-all]:   /images/howitworks-gfx-color-channels-all.png
{: width="100%"}
[channels-red]:   /images/howitworks-gfx-color-channels-red.png
{: width="100%"}
[channels-green]: /images/howitworks-gfx-color-channels-green.png
{: width="100%"}
[channels-blue]:  /images/howitworks-gfx-color-channels-blue.png
{: width="100%"}
[channels-alpha]: /images/howitworks-gfx-color-channels-alpha.png
{: width="100%"}

| ![channels-all] | ![channels-red] | ![channels-green] | ![channels-blue] | ![channels-alpha]
| Silly image     | Channel R (red) | Channel G (green) | Channel B (blue) | Channel A (alpha)

The channels have assigned names and meanings, and that's how image viewers and editors will display them. R, G and B represent colors, A represents opacity (0 means fully transparent, 1 means fully opaque). For more info, see <http://www.howtogeek.com/howto/42393/rgb-cmyk-alpha-what-are-image-channels-and-what-do-they-mean>.

However, the channels are still independent data, and may be used for any purpose. 3D games do this all the time. They often swap color channels around (like ABGR instead of RGBA) or use color channels to store special data for shaders and effects.

# Terrain system

Our terrain system is a good example case. It uses images in 3 specific ways.

## DiffuseSpecular

Primary texture of terrain surface.

RGB channels are used in the usual way - red, green and blue channels of [diffuse map](http://wiki.splashdamage.com/index.php/Basic_Texture_Overview#Diffuse_Maps) (specifies primary color).

The A channel makes it all complicated. It represents a [specular map](http://wiki.splashdamage.com/index.php/Basic_Texture_Overview#Specular_Maps). Because of that, a DiffuseSpecular image will display mostly transparent garbage in an image viewer.

## NormalHeight

Secondary texture of terrain surface.

RGB channels represent a [normal map](http://wiki.polycount.com/wiki/Normal_map). Normal mapping is an essential effect, signifficantly improving visual appearence while being cheap to process.
 
The A channel represents a height map, also called bump-map, eventually parallax-map. In this layer, 0 means lowest area, 1.0 means highest area. This map may be used for [nicer texture blending](https://www.garagegames.com/community/forums/viewthread/134634), but it's primary use is for [parallax mapping](http://wiki.polycount.com/wiki/Parallax_Map).

## Blendmap

This image represents the entire terrain as seen from above, and each color channel specifies areas covered by one texture layer. Value of 0.0 means "no coverage", value of 1.0 means "full coverage".

Mapping between texture layers and color channels is done in configuration file.

# Creating special images

A manual process, may require plugins for your image editor. You need to load all your source graphics to the editor, decompose them to individual channels and then manually re-assemble it to desired form. You need to know what you're doing because the moment you get it "right" for the game, the moment it starts looking "wrong" in the editor.

One editor with built-in support for color channels is [GIMP](http://www.gimp.org/). This is how it decomposes the image above: 
![Color channels in GIMP](/images/gimp-image-color-channels.png)


