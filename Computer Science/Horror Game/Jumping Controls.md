# Jumping Controls
Simply, we go to setting > project setting > Engine > Input > Action Mapping this time. 
We create a method called Jump and set its control with Spacebar

Inside our player blueprint, we set the method
![[Pasted image 20220714120448.png]]

We set it when pressed to `Jump` function and released into `StopJumping` function
![[Pasted image 20220714120556.png]]

We could tweek the built in method `CharacterMovement` to aid us with the height and speed of our jump in Player Movement: Jumping/Falling in Jump Z velocity
![[Pasted image 20220714121031.png]]

![[chrome-capture-2022-6-14 (5).gif]]
