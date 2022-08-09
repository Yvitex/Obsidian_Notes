# Referencing Interaction System'
Sometimes, we need a player reference to the [[Interaction System]] 

We could do this by going into our object actor blueprint. Set the event begin play to the current level [[Creating a Character|game character]] we have using `cast to Level1 Player Character`
![[Pasted image 20220715052520.png]]

Now, we need to get the current player character using the function `get Player Character`
and set it to the object
![[Pasted image 20220715052629.png]]

Promote the cast to a variable
![[Pasted image 20220715052713.png]]

Cgaracter ref will be reused by the child component