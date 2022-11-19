---
aliases: [exposure, inifinite extent, post processing volume]
---
# Setting Up Space
Setup the basic space by creating a new game, applying all addons except [[Ray Tracing]]. 

![[Pasted image 20220714044706.png]]

Create a new Folder called Maps where we will store all Places. On file create new level and choose the default setting
![[Pasted image 20220714044905.png]]

The problem now is that there is a strangeness of changing light intensity when we look down over time. We could cure this by using post processing.
![[chrome-capture-2022-6-14.gif]]

Search for post process volume and place it somewhere in space
![[Pasted image 20220714045038.png]]

![[Pasted image 20220714045159.png]]

Set the exposure > min brightness and max brightness to 1.
![[Pasted image 20220714045237.png]]

Only inside that box the effect will activate but not outside of it. To make it available even outside the box, we enable the *infitnite extent unbound* property
![[Pasted image 20220714045440.png]]

![[chrome-capture-2022-6-14 (1).gif]]