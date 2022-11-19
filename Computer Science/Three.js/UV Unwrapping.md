---
aliases: []
---
# UV Unwrapping

Is the act of converting the 3d [[Three.js Textures|texture]] into 2d space coordinates
![[Pasted image 20220816060449.png]]

And vice versa. 
Inside the [[Three.js Geometry|geometry]] object. we could console log the attribute and we could see the uv attributes in it
![[Pasted image 20220816060642.png]]

This determines the position the 3d object have in 2d space. 

## Blender

### Manual UV Unwrapping
For planes, just select the item, go into edit mode then unwrap all vertices and faces selected. It will produce a box. ![[Pasted image 20220920101149.png]]

For slightly complext object, manual uv unwrapping is the key. Just press the obejct, focus on it using the / key, go to edit mode, select all vertices and faces, press U key as in UV, select `unwrap`
![[Pasted image 20220920101435.png]]

Now as we could see, it is a mess
![[Pasted image 20220920101500.png]]

This happens because their is no way that the software will not automatically create cuts for us. We create the cuts for ourselves. No pain no gain, no cuts no UVs. 

Select a hidden edge to create the cuts
![[Pasted image 20220920101808.png]]
```ad-Notice
title: Choose to cut the material using the edge that is rarely visible
collapse: open
Yes, I don't know why but just to be safe, do this

```
Once we selected the edge, press U, then select mark sean. Once it turns red, then we already made the cut. Once the material is propertly markes, we select the not-so-whole mesh using ctrl + L, press U and then select unwrap

![[Pasted image 20220920102123.png]]

![[Pasted image 20220920102141.png]]

Now it looks somehow proper, do it for the rest of the materials. 
![[Pasted image 20220920103744.png]]

The easiest way is to to mark it first, select all, then unwrap. We also must set some margins for some optimization purposes. Once you are done. you could just duplicate the objects so that you don't need to do it again

![[Pasted image 20220920105110.png]]


Unwrap it again so that they won't have a single unwrapping which is a disaster. It should look like this
![[Pasted image 20220920105202.png]]

The margin is 0.045. 

### Smart UV Unwrapping

An automated way to do stuff, only use it for complex meshes like
![[Pasted image 20220920134045.png]]

Press U then select smart UV Unwrapping. Apply a margin of 0.02 just to separate them
![[Pasted image 20220920134145.png]]

![[Pasted image 20220920134211.png]]

This is good enough. But do this only for complex meshes, i am repeating. Use it for complex meshes, manually doing this is much more optimized. 









# Metatags
###### Related: [[Blender Models]], [[3D Baking]]
###### Tags: #blender 
###### Source: 

---
