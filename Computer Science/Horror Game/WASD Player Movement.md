---
aliases: [add movement input, get actor forward vector, get actor right vector]
---
# Player Movement
We set this up using the [[Creating a Character|game character]] blueprint. First is we create an input like what we done on the [[Camera Movement]]

Go to Setting > Project Setting > Engine > Input > Axis Mapping > Bindings
Then create 2 new methods called `MoveForward` and `MoveRight`. Under the move forward, the controller we use is the keyboard > W, A, S, D depending on their axis. Set the opposite side like down and left to negative scaling because we know that left and bottom is below 0.
![[Pasted image 20220714113207.png]]

Next is to set the [[Creating a Character|game character]] blurprint. Set the 2 methods we just created
![[Pasted image 20220714113344.png]]

Next is to add the value of that method to the `Add Movement Input` method's scale value. This will enable us to move.
![[Pasted image 20220714113508.png]]

But also, we need to properly direct the character to the world, we need to set its direction whether it is going left/right or forward/backward. Therefore we use the `get Actor Forward Vector` for forward and backward direction, then `get Actor Right Vector` for left and right. This is already set to the self or [[Java OOP Methods|this keyword]] in terms of java, which is the current object it occupies so where the camera is looking will be the forward. 

![[Pasted image 20220714113904.png]]

![[chrome-capture-2022-6-14 (4).gif]]

To decrease the speed of the character movement, there is already a builtin method inside the [[Creating a Character|game character]] class. Inside the components, we could see the character movenent,
![[Pasted image 20220714114309.png]]

Under the character movement: Walking, set the max walk speed to 400
![[Pasted image 20220714114418.png]]
