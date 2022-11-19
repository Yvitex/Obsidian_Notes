---
aliases: []
---
# Baking
Is a way for [[Three.js (core)]] to simulate the [[Ray Tracing]] done by other 3d softwares. We will simply extract the [[Three.js Textures]] from rendering in a 3d software then we will apply it to [[Basic Material]] which make it more efficient because we don't need to use [[Three.js Light]]s anymore, except that we need to load some textures.

Use only baking if you don't need [[Three.js Light]]. In blender, we will use the Cycles Renderer
![[Pasted image 20220919024841.png]]

This will enable the [[Ray Tracing]] technique. Now we could start by creating the [[Scene Creation In Blender|scene]]. After this, we need to do some steps in order to optimize the scene we just created. 

## Step 1: Remove Some Faces
First is by removing faces that are not needed or will be hidden from the user. Here, I selected a group of woods
![[Pasted image 20220920050305.png]]

Press / to focus on it. ![[Pasted image 20220920050330.png]]
Go below and delete the hidden faces, this way we could reduce the vertices  to be calculated. 

## Step 2: Make Everything Singular

What this means is that we need to eliminate all linked duplicates (alt + d) and make it all independent meshes. This will enable us to avoid some problems during [[UV Unwrapping]] where we are doing some calculations in the coordinates. When 2 objects are linked, then they will have the same coordinates which is wrong. To do this, select everything in the scene, press f3 then press `make everything singular: object + data`.
![[Pasted image 20220920053611.png]]


## Step 3: Check for Wrongly Oriented Meshes

This are meshes who's faces are looking at the insides rather than the outside. Tich the face orientation at overlays
![[Pasted image 20220920053936.png]]

![[Pasted image 20220920053952.png]]

Red means it is wrongly oriented. To fix this up, select the object then go to edit mode, select all faces, press f3 then search for `recalculate outside` ![[Pasted image 20220920093828.png]]
It will change the orientation automatically. 

## Step 4: Scale Correction

Sometimes we do studpid stuff inside blender, it is recommended to scale the mesh on edit mode rather than in solid mode so that we don't mess up with the scaling. But if you have done this, and you change the scale property from 1 to random float, then we might mess up in our [[UV Unwrapping]] because of wrong scale proportions.
![[Pasted image 20220920094439.png]]

What we could do is to select everything and then use ctrl + a then select scale to return it back to 1 without changing the physical appearance of the meshes
![[Pasted image 20220920094723.png]]




## Step 5: UV Unwrapping

See the lesson about [[UV Unwrapping]] for reference but yeah, for planes and flat surfaces, it will automatically set the UV Unwrapping. We will scale down the Unwrapped texture to a quarted or its original size just to compress all textures into a one single png or jpeg file. ![[Pasted image 20220920101206.png]]
Also take note that we do not need to unwrap the lights, we do this inside the [[Three.js (core)]]. 
If you done your [[UV Unwrapping]] right, then you might have something like this
![[Pasted image 20220920141903.png]]

```ad-Attention
title: Mesh with Emission Material not Included
collapse: open
Take note that we do not uv unwrap the lights or glowing materials, we will redo this effect later directly to the [[Three.js (core)]]

```

We don't know if the scale is similar to each other, what we could do is that in the UV editing mode, we enable the  display strech and set it to `area`
![[Pasted image 20220920142000.png]]

In here we must make all shapes have similar color, similar color means similar proportion. Scale it up or down to do it. Now, once we have all colors conceding each other, go arrange it to fit the box
![[Pasted image 20220920144524.png]]



## Step 6: Baking Powder

Now it is the time to create the actual baking, After you have done your [[UV Unwrapping]], then it is time for you to to create a new image with this properties
![[Pasted image 20220920152805.png]]

Named it as baked. The maximum width and height must be on the power of 2, and 4096 is maximum nothing more as mobile phone cannot handle more than that. Change the color to white, it is just the background but it will help us in some other ways. Tick off the alpha, if we are not using those and then tick 32 bit float for accuracy. 

Save then this image to a folder, as type `radiance hdr` 
![[Pasted image 20220920153124.png]]


This is just the temporary texture that will enable us to be accurate in colors of the texture. We will convert it later to something else. Now, if you have saved you texture as an hdr file, we go to the actual baking.

Open the ==Shader Editor== viewport, and then tick use node. This will show you the basic properties using nodes. Press Ctrl + A and select textures, choose image texture![[Pasted image 20220921041227.png]]

Drop it down in the viewport, don't connect it to other nodes, just let it stay put. Next thing is go to the render section and increase the render sampling to 256, or 128. The more, the better but slower so don't increase it more than 256. 

Now, in the bake section along with the render setting, tick off clear image so that it won't reset everytime we bake the objects. ![[Pasted image 20220921041519.png]]

Execute bake and wait until the progress goes 100%. ![[Pasted image 20220921051838.png]]

After we bake it, notice that there are too much noise and they are in the wrong color. This is because,we have not rendered it with denoising function and also no filmic color encoding. When we render a scene in blender, it shows a filic encoded values along with denoising function, what we could do is to convert the image we got using denoising nodes in the ==compositor== layer

To do this, input a new node called image from input > image then select the baked image. Connect it to the compositor node
![[Pasted image 20220921052320.png]]

Now input a denoising node in between
![[Pasted image 20220921052459.png]]

Sadly, when we rendered it, it goes into a wrong resolution and only render the small portion of it
![[Pasted image 20220921052620.png]]

We could modify these under the output properties setting, our image is orginally 4096 * 4096. Resolution percentage must be 100 percent.
![[Pasted image 20220921053844.png]]

![[Pasted image 20220921053739.png]]

Now that we have this rendered image, we could save it as a jpg, as we don't have alpha and they are quite heavy. Turn down the quality to 75% but it's your choice. Make sure to tick the RGB encoding, not the black and white.

![[Pasted image 20220921054124.png]]

Because, we turned the hdr image to jpg, then the quality might suck. This doesn't matter. 

## Step 7: Export Mesh

The same thign we do for every [[Blender Models]] for [[Three.js (core)]]. Simply go to export and choose [[GLTF]]
![[Pasted image 20220921055037.png]]

Choose gltf Binary or glb. Limit only to selected objects so you need to choose eveyrthing including the emission lights, except camera and area light

![[Pasted image 20220921055203.png]]

We also don't need modifiers, or normals. Disable the vertex colors because we have will use [[Three.js Textures]]. It is important to set the materials to no export, we will going to recreate the materials from scratch. If the compression is working, then use it and we'll going to use [[DracoLoader()]]. Else, then don't.
![[Pasted image 20220921055223.png]]





Now that we finished this, we could now [[Import Baked Material to Three.js]]

# Metatags
###### Related: [[Blender Models]], [[Three.js Scene|scene]], 
###### Tags: #blender 
###### Source: Bruno Simon Tutorial

---