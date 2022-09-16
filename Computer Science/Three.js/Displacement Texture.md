# Displacement Texture
Height or displacement texture - also a grayscale image that move vertices to create some relief
![[Pasted image 20220811133017.png]]

What's happening here is that when we apply this on a [[Three.js Mesh|mesh]], what's happening is that when the area is white, the [[Three.js Geometry|vertices]] will move up and when it is black, the verticess will go down.
This is good for creating terrain and such.

![[Pasted image 20220811133151.png]]

The problem here is that we need more vertices in order to make it work