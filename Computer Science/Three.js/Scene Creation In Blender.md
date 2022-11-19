---
aliases: []
---
# Scene Creation In Blender



![[Pasted image 20220919032946.png]]

## Tip 1: Anti Z-Fighting

Do note that in creating models. there should be no collision of Zed fighting. It will mess with the texture.

## Tip 2: Increase Randomness

Do not make it look so symmatrical. Randomness or inaccuracy, imperfection is perfection.

## Tip 3: Origin Point

If we go to edit mode and move the vertices, the origin point will not follow along. Make use of it to modify origin of scaling. Also, when scaling or rotating, we must go into edit mode before doing so. 

## Tip 4: Triangle 

On a flat surface, we could use the n-gon meshes. But when creating a mesh with non flat surface, then we should use triangle fan setting so that it would be triangle which is a predictable mesh when imported to [[Three.js (core)]], or else, quads or 4 vertices like box which could be split into triangles. 

![[Pasted image 20220919052011.png]]


## Tip 5: Collection

It is a good practice to store every meshes in the designated folder like collections

![[Pasted image 20220919062059.png]]

This way we could easily hide and deselect objects. We could also modify the toggle and activate the select and deselect enabler
![[Pasted image 20220919062148.png]]

Once you have your scene:
![[Pasted image 20220920034854.png]]

We could now apply some materials. Go to material previews, select an object, rename the material class then apply the properties to the material.
![[Pasted image 20220920035226.png]]

Now that we applied some properties to the material, we could select multiple ones and the select an object with already defined properties, press ctrl + l and then link materials. 

For lights, we shall use instead of Principled BSDF, we use Emission Material
![[Pasted image 20220920041611.png]]

This will add some glow to the material. 
![[Pasted image 20220920042644.png]]

What else could we do but to change the point light we have to a directional or area light enabling diffusion? Also we cound enable the denoising function

![[Pasted image 20220920044520.png]]


# Metatags
###### Related: [[Blender Models]], [[3D Baking]]
###### Tags: #blender 
###### Source: 

---
