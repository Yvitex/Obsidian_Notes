---
aliases: [add pitch input, add yaw input, pitch, yaw]
---

# Camera Navigation
We created  it by coding [[Creating Player Controller|Player Controller]]. 

## Setup
We first create our own input method in the project setting. First, find the input under the Engine setting
![[Pasted image 20220714104240.png]]

Inside this, under the bindings, create a 2 new axis mapping that will handle 2 of our methods, the `LookUp` method and `LookLeft` method and bind it to the mouse in its own axis.
![[Pasted image 20220714104308.png]]

Also, we set the scale of y into a negative value. This is like what we do in [[Moving Camera By Mouse]] in three.js
![[Pasted image 20220714104416.png]]

Now, access the [[Creating a Character|game character]] blueprint and press the poperties of the camera. Tick the *Use Pawn Control Rotation* on under the Camera Options
![[Pasted image 20220714105104.png]]

Inside the [[Creating Player Controller|Player Controller]] blueprint, import our method `LookUp` and `LookLeft`
![[Pasted image 20220714105255.png]]

Apparently, the Name is appended with Input string, For the Y value, we must set it to the `AddPitchInput` and the X to the `AddYawInput`
![[Pasted image 20220714105432.png]]

But as we could see, it is farr too sensitive, we must wane it using a variable. 
Create a new variable and set it to float, make the value at least 0.4 and multiply it to the Axis value and set it to the pitch and yaw
![[chrome-capture-2022-6-14 (3).gif]]

