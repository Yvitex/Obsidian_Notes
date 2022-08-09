---
aliases: [line trace, interaction interface, LineTraceByChannel, getWorldLocation, Break Hit result, get Forward Vector, Does Implement Interface, isValid, blueprint interaction actor]
---
# Interaction System
Sumply interacting with objects in an environment inside a game

The basic process is creating an interaction system involves action method -> create an interface -> create a line trace -> applying interface to an object -> debugging

First is to create an action method that will activate when we press the keyboard e, we could do this similarly to how we create  the [[Jumping Controls]]. Go to setting > project setting > engine > input > action mapping. Create a method called `Interact` or `Action` or some sort, then map the button e
![[Pasted image 20220714151429.png]]

Create anothe blueprint folder that will store our other blueprints aside from the basic game blue print. Create another folder called Interface where we will store the interfaces. Create a new blueprint with a type of **Blueprint Interface**
![[Pasted image 20220714151604.png]]

Rename it as BPI_Interaction or whatever. Inside this new class, create a new function called interact. ![[Pasted image 20220714151744.png]]

We created an action method and created an interface, next step is to create a line tracer that will detect an object when it is in front of us. 
Inside the [[Creating a Character|game character]] blueprint, we create a new function called `Line Trace`, it will have a parameter of float where we specify the length of our line so we call this parameter `length`
![[Pasted image 20220714152127.png]]

Next method to establish is the builtin, `LineTraceByChannel` function. This will be the actual line trace we have, though it will need 2 values, a line consist of 2 points, therefore we need to specify the starting position and the ending position. ![[Pasted image 20220714152400.png]]
The starting point needs a vector value, the line trace must start with the camera so therfore, we need to get the location of the camera and use this as the starting value. We do this using the function, `getWorldLocation`
![[Pasted image 20220714152554.png]]

The ending location has a tricky calculation, we first need to determien which way is forward using the function `get Forward Vector`, we multiply this by the value of our `length` parameter then adding it to the world location of the camera (vector + vector). This will be the end point of the line trace
![[Pasted image 20220714153857.png]]

We expect the `line trace` function to return somethis, so we add a return statement to return an object that will be hit by the line trace. Name that return variable as Hit Actor
![[Pasted image 20220714154246.png]]

We could detect the object hitted by this line trace using the `Break Hit result` only available in `out Hit`
![[Pasted image 20220714154419.png]]

Now, we will utilize the method we created using e keyboard. Use the `Interaction` method. When it is pressed, we will execute the `Line Trace` function we just created. Set the length to any value, suggested is 350
![[Pasted image 20220714154850.png]]

Next is to enable that, when we press e, it will create a line trace, if line trace hits an actor it will execute an event for that object, the target is what line trace is returning
![[Pasted image 20220714155156.png]]

This is all fine and good but we will implement another layer of security by implementing a conditional statement, if the hit actor is a valid actor and an object with BPI_Interface, then and only then we will execute the event, we could do this using a `branch` which will handle the conditional statement, `isValid` function and `Does Implement Interface` function with `and` logical expression
![[Pasted image 20220714155607.png]]

Now... Create a new folder for actors. Create a new blueprint only for actors. Inside it, implement an interface which we have created called `BPI_Interact`, we could find this at Class Setting > Interfaces > Implement Interface. And place a mesh, at least a cube just for debugging. 
![[Pasted image 20220714160127.png]]![[Pasted image 20220714160137.png]]

Inside the script, place a new event using the `Interact` Blueprint Interface, when this event is triggered, we will print a string called `Hello`
![[chrome-capture-2022-6-14 (6).gif]]
