---
aliases: [create widget, add to viewport]
---
#  Crosshair
Is a nice addition to the [[Interaction System]], simply it is a dot or a cross in the center of the screen like a widget

Create a folder called texture. Inside this, import the the texture image of the crosshair, it must be a 5 by 5 pixel square white box.  Set the compression setting and texture group of the image to [[User Interface Basics|UI]]. ![[Pasted image 20220714165534.png]]
![[Pasted image 20220714165555.png]]

Create a nee folder called UMG, create two user interface > Widget Blue print, One is the main widget where we will apply all widget, name it as `MainHUD` and the next one is the `Crosshair_widget` 
![[Pasted image 20220714165801.png]]

Inside the crosshair widget, we do not need it to be the same size as the viewport, infact, we want it to be resized by us, therefore, first delete the canvas panel
![[Pasted image 20220714165914.png]]

Then apply `Size Box` and inside it is an `Image`. Inside the image property, use the brush to select a texture then apply it to the image. 
![[Pasted image 20220714170138.png]]

It is only a 5 by 5 image so the size box must also be the same, set the max height and width to 5 by 5 ![[Pasted image 20220714170105.png]]

Add this to the MainHud blueprint. In the palete of main hud, look for the user created palete, we will find there the Crosshair_widget we just created
![[Pasted image 20220714170638.png]]

Add it then resize to 5 by 5 image. Anchor it to the center of the screen with the help of `anchor` by centering it, set the x and y value to 0 and also align it to 0.5 in both x and y
![[Pasted image 20220714170815.png]]


Now, inside our [[Creating a Character|game character]] blueprint, under the `event begin play` which will execute in every start of the game, we will create a new function that will add our created widget to the screen. Call this initialize_crosshair.

We will then create a widget by calling `Create Widget` then set the class to Main_HUD. Set the return value to a variable main_hud as we are reusing it later on then use the function `add to viewport` to add it to the screen.
![[Pasted image 20220714171230.png]]

Tick it to the begin event
![[Pasted image 20220714171247.png]]

![[chrome-capture-2022-6-14 (7).gif]]