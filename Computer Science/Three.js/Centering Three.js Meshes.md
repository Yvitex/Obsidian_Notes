# Centering Meshes
Here we use the example for [[Three.js Text Geometry]]. 
![[Pasted image 20220817112614.png]]

It is not centered shown by our axes helper. 
There are several ways to center it, first is using the [[Bounding]]
As we could see using the axes helper
![[Pasted image 20220817140910.png]]

There is a lready some extra space that goes beyong the origin (0, 0). It is because of the Bevel size applied in the [[Three.js Text Geometry]]. Wecould see this using a [[Bounding]] calculation called using the [[Three.js Text Geometry]]'s method called `computeBoundingBox()`

```js
textGeometry.computeBoundingBox()
```

After this, we could console log the boundingBox text geometry's property
```js
textGeometry.computeBoundingBox()
console.log(textGeometry.boundingBox)
```

What outputs is this
![[Pasted image 20220817141342.png]]

This shiws that the size of the bounding box exceeds the origin point by 0.02. What we could do to center it is to divide the max value of the bounding box by 2 and after substracting it by 0.02 using `translate`

```js
textGeometry.translate(
          - (textGeometry.boundingBox.max.x - textGeometry.boundingBox.min.x) * 0.5,
          - (textGeometry.boundingBox.max.y - textGeometry.boundingBox.min.y) * 0.5,
          - (textGeometry.boundingBox.max.z - textGeometry.boundingBox.min.z) * 0.5
        )
```

![[Pasted image 20220817142356.png]]


Or instead, to make this short, just use the [[Three.js Text Geometry]] property called `.center()`
```js
textGeometry.center()
```

Both method will produce the a good result in the boundingBox property
![[Pasted image 20220817142750.png]]

