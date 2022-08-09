---
aliases: [lerp, box simplified collision, create timeline, set relative rotation, make rotator]
---
# Opening Doors
We utilize what we learned in [[Interaction System]]. After creating a [[Interaction System|blueprint interaction actor]], we could just simply create a child of that component![[Pasted image 20220715055950.png]]

Rename it as BPI_InteractDoor. Inside this child component, Change the Cube mesh into the Door Frame mesh and also reset the material to default![[Pasted image 20220715060236.png]]

Next step is the door, create a new child of the cube static mesh which is another static mesh and change it to the actual door and allign it with the frame
![[Pasted image 20220715060458.png]]

Because it is only a child of the Interact Actor component we created on the [[Interaction System]], it alsready have an interface, We just need to create an event using it. To test it, print a string.
![[chrome-capture-2022-6-15.gif]]

As we could see, it doesn;t work, and also we pass through the door, It is because we have no collision applied to the door,
![[Pasted image 20220715061239.png]]

Goto the door mesh, under the collision , add a box simplified collision
![[Pasted image 20220715061315.png]]

Modify the width and height, thichness of collision box under collision propertu > primitives > boxes >  x/y/z extent
![[Pasted image 20220715061557.png]]

Now we could see the fruit of our labor.
![[chrome-capture-2022-6-15 (1).gif]]

To  open the door, we need to rotate it -90 degrees in the z axis
![[Pasted image 20220715061726.png]]

And we know, there is a time it takes when an action happens, it is an animation, therefore we need a timeline that will handle the time seconds of action. Create a timeline using `Add Timeline` and rename it as Door Timeline

![[Pasted image 20220715062032.png]]

Set the timeline in length 0.5 which is the time it takes for the door to open
![[Pasted image 20220715062016.png]]

Create a new function plot, set 2 points in time. The first point is on time 0 with value 0 and second point on time 0.5 max and value 1. Like [[Binary]]
![[Pasted image 20220715062224.png]]

The thing we need to rotate is the door mesh, import it to the code
![[Pasted image 20220715062400.png]]

To rotate it, we need the function `setRelativeRotation` 
![[Pasted image 20220715062453.png]]

The only thing we need to rotate is the z axis, we need to sepatate the axis using `makeRotator` 
![[Pasted image 20220715062709.png]]

So, [[Camera Movement|yaw]] is actually the z axis?
We know that the alpha only return values in range 0 and 1, which is not a proper value for our axis, i mean we could but we already know we need to rotate the door 0 to -90 degrees not 0 to 1. We need to convert it from 0 to 1 to 0 to -90 degrees, we could do this using function `Lerp`
![[Pasted image 20220715063244.png]]

It accepts 3 value, the first 2 is the range of convertion, 0 and -90 then the alpha which is any value, in our case, a range between 0 and 1.
![[chrome-capture-2022-6-15 (2).gif]]

It now works, but we can;t close it, we could close it using the reverse function of our timeline, but the problem is, we need to check when the door is closed or not, we need to create a boolean variable that wll hold the door state.
![[Pasted image 20220715063648.png]]

![[chrome-capture-2022-6-15 (3).gif]]

There are more advance ways on doing this, we could create this effect, where the door could open in either sides, read [[Creating Advance Door Opening]]
