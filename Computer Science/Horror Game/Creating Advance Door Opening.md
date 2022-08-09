# Creating Advance door animation
From what we created in the basic door motion called [[Opening and Closing Door]]. We will append only additional codes. duplicate the door actor blueprint we created in that section
Open the blueprint and review the codes
![[Pasted image 20220715094623.png]]

To detect where we are located in the game and also the door, we must get the reference with those 2, get the player reference and the door reference using the `self`. Player reference variable is created in the [[Referencing Interaction System]]  and is inherited by the child component
![[Pasted image 20220715094904.png]]

Get both of their location using the `get Actor Location`
![[Pasted image 20220715094955.png]]

Substract both of their location then `Normalize`. normalizing it will enable the coordinate have a maximum vector value of 1 which is easier to track. This is called unit vector
![[Pasted image 20220715095511.png]]

Next is we need to get the [[Dot Product]]  in order to reference if we are looking in the front of the door or at the back, this will return a range of numbers from 1 to -1. We will yse the normalize coordinate of the door object and its forward vector using [[Interaction System|get Forward Vector]] , set the [[Dot Product]] to a variable that will be executed after branch conditional statement
![[Pasted image 20220715104602.png]]

We will use this [[Dot Product]] to check if it is less than 0 or greater than 0, in our [[Opening and Closing Door|lerp]], we will modify it with `select`, where  in we will change the rotation of the static mesh not only in -90 degrees but also 90 degrees. We will use our reference variable [[Dot Product]] to check if it is greater than or equals to 0 and if true, we will rotate it by 90 degrees
![[Pasted image 20220715105214.png]]

We shall not use the actual [[Dot Product]] but the variable as it will update immediately causing a glitch to how the door moves
![[chrome-capture-2022-6-15 (4).gif]]

Unlike when we do the right connecttion, the variable will be saved after setting the boolean `isDoorOpen` to false. 
![[chrome-capture-2022-6-15 (5).gif]]