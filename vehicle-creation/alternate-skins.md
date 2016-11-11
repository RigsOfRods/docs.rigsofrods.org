---
title: "Making alternate skins"
layout: page
categories: [vehicle-creation]
---


This page serves as an overview page o how to create and modify custom skins.

# Step-by-step guide

## Step 1 - GUID

Skins are matched against vehicles via GUID (Globally-Unique-IDentifier).
Make sure the vehicle you want to skin has one: [/technical/fileformat-truck#guid]
Ideally, all trucks should have one. You might need to clear the cache, so the GUID will be in the cache as well. 
You could generate some GUIDs there: http://www.guidgenerator.com/.

## Step 2 - the .skin file

Create a file named "MySkinName.skin" (replace MySkinName with any String without spaces) with the following content:

    Sarens Skin for Sennebogen 5500
    {
    	replaceTexture   = blansjaar41.jpg, blansjaar41_sarens.jpg
    	preview          = 9c15cccf8a8dca392b84b7b778e3517139cef287.png
    	description      = sarens skin for the sennebogen 5500
    	authorName       = Rotexx
    	AuthorID         = 39570
    	GUID             = 90670430-695d-467b-8c91-dcb67a42633c
    }

this skin was made by Rotexx whose Author ID is 39570. 
The preview image for the skin is 9c15cccf8a8dca392b84b7b778e3517139cef287.png.

There are 2 ways how to replace the original vehicle graphics with yours:

* **Image substitution** - The simple one, you name an existing texture
    file and a replacement file. In this example,
     'blansjaar41.jpg' is replaced with 'blansjaar41_sarens.jpg' 

* **Material substitution** - More complex, you need to know the .material
    file format of OGRE3D engine. For an example, see the "antonov" tutorial
    below. The principle is the same - you name the original material and then
    the new, replacement material.

## Step 3 - the package

Put all the files into a zip archive named "sarens.skinzip" 
and put that into the packs folder (NOT .skinzip.zip, just .skinzip). 
The .skinzip is important, as it will force RoR to always load this zip 
to parse the skin information from it.

## Step 4 - the game

Start the game and select the truck, it should have a valid GUID in the selection menu. 
When pressing enter, the skin selection GUI will be displayed.

# Skin file reference

    Sarens Skin for Sennebogen 5500
    {
    	// this is a comment line, it is ignored when parsing. It always starts with //
    	// replaceTexture = <original_texture.png> <skin_texture.png>
    	replaceTexture   = blansjaar41.jpg, blansjaar41_sarens.jpg
    	replaceTexture   = blansjaarkleur.jpg, blansjaarkleur_sarens.jpg
    	replaceTexture   = blansjaarlogo5500.jpg, blansjaarlogo5500_sarens.jpg
    	// replaceMaterial = <originalMaterialName> <skinMaterialName>
    	// preview = <preview_image.png>
    	preview          = 9c15cccf8a8dca392b84b7b778e3517139cef287.png
    	// description = text that will show in the selectionWindow
    	description      = sarens skin for the sennebogen 5500
    	// AuthorName = <author name, no special characters>
    	authorName       = Rotexx
    	// AuthorID = <forum ID of the author>
    	AuthorID         = 39570
    	// GUID = <of the truck to which this skin fits>
    	GUID             = 90670430-695d-467b-8c91-dcb67a42633c
    }


'''replaceTexture''' defines the texture replacements, its first argument is 
the original texture name, the second argument is the texture name of the skin. 
Please note that those must be different, or you will get a file collision. 
You can use this line as much as you like.

''' // ''' is the comment keyword

'''GUID''' will refer to the truck's GUID.

'''c)''' put all the files into a zip archive named "sarens.skinzip" and 
put that into the packs folder. The .skinzip is important, as it will force RoR 
to always load this zip to parse the skin information from it.

'''d)''' start the game and select the truck, it should have a valid GUID in 
the selection menu. When pressing enter, the skin selection GUI will be displayed.

'''How to test the fast way (how to use the attached files):'''

Download them all into your packs folder, do not unpack them. 
Delete any old "sennebogen5500" versions.

# Another guide (Antonov)

So for an example we will just do this now for the an-12.airplane.

[antonov-thumb]: /images/skins-example-antonov.png
{: }

![antonov-thumb] 

## Step 1 - The material

create a very simple skin material file without anything special:

    material my-green-antonov-skin
    {
    	technique
    	{
    		pass
    		{
    			scene_blend alpha_blend
    			alpha_rejection greater 128 
    			texture_unit
    			{
    				texture my_antonov_texture.dds
    			}
    		}
    	}
    }

## Step 2 - The .skin file

To find out the original material name, 
open the an-12.airplane (in data/trucks/), find the globals section 
and note down the third argument ('''tracks/An12''') 

Then create a simple .skin file to describe the skin:

    Antonov 12 - Green Skin
    {
        // GUID (globally unique identifier), REQUIRED!
        GUID = ...GUID, see above...
        // Forum ID of the author, optional
    	AuthorID = 1
        // Name of the author, optional
    	AuthorName = Thomas
        // Preview image. Must be 256x256 pixels big and should be in dds format.
    	Thumbnail = an-12-skin-mini.png
        // The substitution: old material name, new material name
    	replaceMaterial = tracks/An12 my-green-antonov-skin
    }

this will replace the old material name (take the names from step 1) with 
the new material (from step 3)<br> If you want to replace more than 
one materials (for example for the props or anything else, 
just add lines with the correct format. 

## Steps 3,4

Like above - package your skin files to .skinzip, and enjoy it ingame!

## More examples

    Antonov 12 - Green Skin
    {
    	SkinType Vehicle
    	AuthorID 1
    	AuthorName Thomas
    	Thumbnail an-12-skin-mini.png
    	// basic version:
    	replaceMaterial tracks/An12 tracks/An12-skin
    }
    
    Antonov 12 - Red Skin
    {
    	SkinType Vehicle
    	AuthorID 1
    	AuthorName Thomas
    	Thumbnail an-12-skin-mini.png
    	// basic version
    	replaceMaterial tracks/An12 tracks/An12-skin
    	// enhanced version:
    	replaceMaterial tracks/An12-En tracks/An12-skin
    }
    
    Antonov 12 - Blue Skin
    {
    	SkinType Vehicle
    	AuthorID 1
    	AuthorName Thomas
    	Thumbnail an-12-skin-mini.png
    	replaceMaterial tracks/An12 tracks/An12-skin
    }

