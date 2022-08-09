# Illustrator to Animation
In illustrator, just simply save the illustration as an [[Scalable Vector Graphics|svg]] file. Try to open it as text and copy it to the [[HTML]]

![[Pasted image 20220712053952.png]]

I downloaded the illustrator software at [getintopc](https://getintopc.com/), then i exported this as an [[SVG]]
Save as > [[SVG]] > [[SVG]] code
![[Pasted image 20220712054122.png]]

Copy this to [[HTML]]

We could use the motionPath plugin for this
```js
https://cdnjs.cloudflare.com/ajax/libs/gsap/3.10.4/gsap.min.js
https://cdnjs.cloudflare.com/ajax/libs/gsap/3.10.4/MotionPathPlugin.min.js
```

To utilize this, we simply use motionPath as one of the propertues in [[GSAP Programming|tweening]]
```js
gsap.to("#ball", {duration: 6, motionPath: {
	path: "#path",
	align: "#ball"
}})
```

Path is the id of the line path and ball is the id of the circular element.
![[chrome-capture-2022-6-12 (3).gif]]
