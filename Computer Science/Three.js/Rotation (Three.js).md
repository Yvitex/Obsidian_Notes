---
aliases: [rotation, quarternion]
---
# Rotation
Like [[Position (Three.js)|position]], and [[Scale (Three.js)|scale]], this utilizes the xyz coordinate system but instead of [[Vector3]], this uses [[Euler's Angle]]

So basically if we have a [[Three.js Mesh|mesh]], we could rotate it by
```
mesh.rotation.x = 1
```

![[Pasted image 20220611061712.png]]

But keep in mind that rotating it by x won't rotate it in the x axis, but rather to the y. Why? Because it is on [[Euler's Angle|euler's]]. A technique to imagine this is to have a string attached to the x axis, so that when we rotate it, will rotate in the y direction. 

And also, 1 revolution is equal to 2pi. Meaning, half rotation is equals to 3.14159 but because we are in [[JavaScript]], we could use math function called `Math.PI` 

```
mesh.rotation.x = Math.PI * 0.5
```
![[Pasted image 20220611061742.png]]
Will rotate the mesh by 1/4 as we are multiplying half rotation by 50%.  

```
mesh.rotation.x = Math.PI * 0.25
mesh.rotation.y = Math.PI * 0.25
```

![[Pasted image 20220611061823.png]]


#three