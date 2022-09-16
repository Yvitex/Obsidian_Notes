# Creating Models
Here we will create hamburger in blender
The first thing you need to mind is the unit. Of you are creating just a small items, then we must do create it in cm rather than in meters
![[Pasted image 20220825161956.png]]

What we could do is change the units to none in the scene panel
![[Pasted image 20220825162040.png]]

Then just imagine that we are working in cm. 
Protip, if we are scaling items, make sure that it is on edit mode so that we don't mess with the scaling
![[Pasted image 20220825162144.png]]

The scale must always be 1. 
Sometimes, you might always want to start with a box, then apply a subdivision surface and make it a sphere, subdivision surface always result into sphere
![[Pasted image 20220825163337.png]]

Add more subdivision to make it actualla sphere then shade smooth
![[Pasted image 20220825163557.png]]

scale the face in compression then apply some loop cuts using ctrl r
![[Pasted image 20220825163737.png]]

Flatten it more
![[Pasted image 20220825164018.png]]

Create patty by reshaping and duplicating the layer
![[Pasted image 20220825170003.png]]

Add cheese by creating a plane
![[Pasted image 20220825170127.png]]

Add more subdivision, and make it look like the cheese is melting
ADD top buns then materials color. voila
![[Pasted image 20220825173141.png]]
 
 Burgeris de puta

 Now to export it, choose the model
![[Pasted image 20220825175206.png]]

Choose the gltf exporter
 ![[Pasted image 20220825175036.png]]


Choose the following parameters
![[Pasted image 20220825175343.png]]

We are just going to limit to the selected objects, y+up is just inverting the z and the y to make it compatible when [[Three.js Imported Models|imported models]] in three.js. We also apply the modifier and deselect uvs because we are not using one, 

If you want the compressed version using draco then tick the compressed
```ad-Danger
title: Compression Error
collapse: open
I don't know how to fix the `nonetype has no attribute data`

```

Export it.
![[Pasted image 20220825180537.png]]

![[Pasted image 20220825181542.png]]

It's heinous. It;s not realistic, maybe we could actually modify it to create a much more [[Realistic Rendering]]
