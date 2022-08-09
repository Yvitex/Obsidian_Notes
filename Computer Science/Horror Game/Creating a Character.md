---
aliases: [game character]
---

# Character Creation
Is a type of spawn which could walk around the game using a [[Creating Player Controller|Player Controller]]

## Setup
Go to the blueprint folder, inside the level folder create a new class using character
![[Pasted image 20220714095012.png]]

Rename the character as the current level + _Character

Double Click the new Character class to configure it. Move the camera to z : 60 position to make the camera in eye level of that of a human as we are making a first person controls the compile
![[Pasted image 20220714095318.png]]

Next is to add the player inside the [[Creating Game Modes|game mode]], inside the classes in the default pawn class, change it to the created Character class
![[Pasted image 20220714095450.png]]

Check if it is working by printing a string using print string in the event begin play node
![[Pasted image 20220714095556.png]]

![[chrome-capture-2022-6-14 (2).gif]]

