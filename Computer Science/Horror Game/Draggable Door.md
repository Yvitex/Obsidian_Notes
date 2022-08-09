# Physics Door
A more complicated code and not very fun to create.

The first step is to create a new folder inside the blueprint folder called Actors, and inside this, create a new folder called Draggable. In here create a new door from scratch using static meshes, you can use the [[Opening and Closing Door]] as a reference. We don't need to create from a parent component as we are using a new different interface,
![[Pasted image 20220715144725.png]]

Next is to enable the physics of this door. Under the physics property, enable simulate physics, angular damping into 4 to create a angular effect, lock the position in x y and z, and lock rotation by x and y, we will only chnage the z axis.
![[Pasted image 20220715144929.png]]

Add a *physics constrains* to the door
![[Pasted image 20220715145018.png]]

Make sure the naming of your static meshes are appropriate
![[Pasted image 20220715145221.png]]

Set the constrains of physics constraint in the DoorFrame and the Door, set their behavior to disable collision to prevent a glitch when opening it, 
![[Pasted image 20220715145310.png]]

Lock all angular limits exept 1 where we limit it to 90 degrees which is enough for the door to open completely.
![[Pasted image 20220715145407.png]]

Check if the physics is applied.
![[chrome-capture-2022-6-15 (6).gif]]

Now, in the interface folder, create a new [[Interaction System|interaction interface]] which is now draggable. In here, create 2 new functions called drag object and release object
![[Pasted image 20220715145758.png]]

In the input settings, you know where from the [[Camera Movement]]. We create a new method using left mouse click
![[Pasted image 20220715145901.png]]

Using this, create a new input inside the [[Creating a Character|game character]] blueprint
![[Pasted image 20220715150102.png]]

We will create a [[Interaction System|line trace]] to that input, because we already create a function, there is no reason to recreate the same code twice. 
The next thing we need to do is to check when the code [[Interaction System|isValid]] and [[Interaction System|Does Implement Interface]] called draggable which we created. Set the hit object to a variable and if all condition is true, call the Drag Object Function in the Draggable interface.

![[Pasted image 20220715151549.png]]

Check if this is working by implementing the interface inside the door actor. Then calling the event DragObject with a print string ![[Pasted image 20220715151738.png]]
![[chrome-capture-2022-6-15 (7).gif]]

What we need to now, is when we are trying to drag an object, we will disable the player movement and also disable the camera. First is to disable character movement, we could do this by calling the `get Player Character` method, extracting the movement status using `get Character Movement` and disabling it using `Disable Movement`
![[Pasted image 20220715152139.png]]

Next is to ignore the camera input, we could do this by calling the `get Player Controller` which will reference to our controller then disabling the navigation by calling `Set Ignore Look Input` ![[Pasted image 20220715152338.png]]
Next is to enable the control to the Door Actor by calling `Enable Input`, set the player controller to our current player controller.
![[Pasted image 20220715152459.png]]

In the same blueprint, create a new Event called MoveDoor using `Custom Event`
THis must have an input parameter of rotation value, which is dependent on our mouse
![[Pasted image 20220715152800.png]]

Get the target door object and set is a target for a relative rotation.![[Pasted image 20220715153151.png]]

Create a rotator, then add the value of the input parameter Rotation value to the relative rotation of the static mesh Door using `Combine Rotator`, and `get Relative Rotation`, also don;t forget the [[Opening and Closing Door|make rotator]] that will separate the z axis to the rest axis
![[Pasted image 20220715153335.png]]

Now, to input the values tothe rotation value, we re use the [[Camera Movement]]'s MoreRight method.
![[Pasted image 20220715153526.png]]

![[Pasted image 20220715154110.png]]

We also implement the algorithm from the [[Creating Advance Door Opening]] to check weather the person is in the front or back of the door. If the [[Dot Product]] is positive, we will multiply the Input Parameter with 1, if not, we will multiply it with -1 reversing the orientation of the mouse.

We could also decrease the sensitivity of the door, by multiplying the mouse input with a decimal number
![[Pasted image 20220715154402.png]]


Now to create what will happen if we release the left mouse click, we go again to our [[Creating a Character|game character]] blueprint, and into the release method of the ActionLCD, check if there is a valid draggable object then release it by setting the variable to empty and then calling the event release object
![[Pasted image 20220715162153.png]]


Into the release object event, we must make the player move again, regain the controls of the camera and disable the input control of the door.
We could set the movement again by calling the player reference then the `set Movement Mode` to walking
![[Pasted image 20220715161625.png]]

Next is to reset look input using `Reset Ignore Look Input` in the player controller reference.
![[Pasted image 20220715161738.png]]


Next is to disable the input using `Disable Input`
![[Pasted image 20220715161834.png]]


![[chrome-capture-2022-6-15 (8).gif]]