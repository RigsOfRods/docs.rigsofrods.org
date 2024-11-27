Shadows
============



As of version 0.4.5.0, Rigs of Rods uses the PSSM (Parallel-split Shadow Maps) shadows technique. 

Shadow textures are split into 3 different textures with different resolutions and sizes. 

The closest one to the camera is the smallest and has the biggest resolution. 
The second and the thirds are sometimes equal in resolution but not in size. 

Shadow details progressively degrade as soon as you get into the 2nd and 3rd split.

## How to make your models receive shadows

### Objects

On the 1st line of the material file, put this line of code:
```
import * from "managed_mats.material"
```

If you want to go simple, you can do it this way:
```
material material_name_here: RoR/Managed_Mats/Base
{
	set_texture_alias diffuse_tex texture_name_here.dds
}
```
Do not forget to add the `: RoR/Managed_Mats/Base` after the material's name.

Or for more control over the material file, you can do it this way:

```
material material_name_here: RoR/Managed_Mats/Base
{
	technique BaseTechnique
	{
		pass BaseRender
		{
			//Ambient, diffuse, emissive stuff here

			texture_unit Diffuse_Map
			{
				texture texture_name_here.dds
			}
		}
	}
}
```
Notice here that in addition to the `: RoR/Managed_Mats/Base`, the technique has a defined name `BaseTechnique`, the pass has a defined name `BaseRender`, and the texture has a defined name `Diffuse_Map`.

As soon as you put all these three, you will get working shadows with a detailed material file. You can still add as many techniques/passes as you want but do not use the same names again, you can simply not name them.

### Vehicles

Shadows no longer cast onto vehicles as of version 2022.12+  due to [graphical glitches](../gameplay/common-issues.md#flickering-vehicle-shadows).

### Misc
Other than the `RoR/Managed_Mats/Base` inheritance, you can use all these for each type of texture/model used.

```
RoR/Managed_Mats/Base
RoR/Managed_Mats/BaseNoShadows
RoR/Managed_Mats/BaseSpecular
RoR/Managed_Mats/Vegetation
RoR/Managed_Mats/Transparent
```

You can take a look at `Rigs of Rods/resources/managed_materials/managed_mats.material` for more understanding of how it all works.



