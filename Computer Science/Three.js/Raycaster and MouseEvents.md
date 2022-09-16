---
aliases: [raycaster.setFromCamera()]
---
# Raycaster and MouseEvents
The first thing we need to do is to locate the coordinate of mouse
To do this, create a new Vector2 in [[Three.js (core)]]
```js
const mouseCoor = new THREE.Vector2()
```

Add an event listener that will modify the mouseCoor Vector 2 values. 
```js
window.addEventListener("mousemove", () => {

})
```

Mousemove [[Javascript|Js event listener]] have a callback called events and this event will contain the lcoation of the mouse
```js
window.addEventListener("mousemove", (event) => {
	mouseCoor.x = event.clientX
	mouseCoor.y = event.clientX
})
```

If we consolelog the value of mouseCoor, we will see this
![[Pasted image 20220823054139.png]]

What we need is the normalized version of it from -1 to +1
To do this. divide by the browser's width and height. The variable below are from [[Fullscreen Mode]]
```js
window.addEventListener("mousemove", (event) => {
	mouseCoor.x = event.clientX / sizes.width
	mouseCoor.y = event.clientX / sizes.height
})
```

Now we will have values from 0 to 1. 
![[Pasted image 20220823054237.png]]

Multiply it by 2 and substract by 1
```js
window.addEventListener("mousemove", (event) => {
	mouseCoor.x = event.clientX / sizes.width * 2 - 1  
	mouseCoor.y = event.clientX / sizes.height * 2 - 1 
})
```

![[Pasted image 20220823054533.png]]

Now the problem is that when the mouse goes up, y became negative which is wrong. We need to reverse it.
```js
window.addEventListener("mousemove", (event) => {
	mouseCoor.x = event.clientX / sizes.width * 2 - 1  
	mouseCoor.y = (event.clientX / sizes.height * 2 - 1) * -1
})
```

Now that we have our coordinates, it is time tocreate a ray caster instance
```js
const raycaster = new THREE.Raycaster()
```

Because we need to check the raycaster for each frame, we must test it inside the tick function of te [[Three.js Animations]]
```js
tick = () => {
	const elapsedTime = clock.getElapsedTime()

	// Animation
    object1.position.y = Math.sin(elapsedTime * 0.3) * 1.5
    object2.position.y = Math.sin(elapsedTime * 0.8) * 1.5
    object3.position.y = Math.sin(elapsedTime * 1.4) * 1.5
    
	controls.update()
	renderer.render(camera, scene)
	window.requestAnimationFrame(tick)
}
```

So what we could do is to call the raycaster method called `setFromCamera()`
here we will pass 2 method which is the camera and the coordinates, or mouse coordinates, then change the color of the material property
```js
tick = () => {
	const elapsedTime = clock.getElapsedTime()

	// Animation
    object1.position.y = Math.sin(elapsedTime * 0.3) * 1.5
    object2.position.y = Math.sin(elapsedTime * 0.8) * 1.5
    object3.position.y = Math.sin(elapsedTime * 1.4) * 1.5

	const targets = [object1, object2, object3]
	raycaster.setFromCamera(mouseCoor, camera)
	const intersects = raycaster.intersectObjects(target)
	
	for (let object of targets) {
		object.material.color.set("#f00")
	}

	for (let intersect of intersects) {
		intersect.object.material.color.set("#00f")
	}
    
	controls.update()
	renderer.render(camera, scene)
	window.requestAnimationFrame(tick)
}
```

![[chrome-capture-2022-7-23s.gif]]


To go futher, beyong using for loops just to detect the mouse enter and leave. we could use a witness variable to do this 
```js

let witness = null
const tick = () =>

{
	const elapsedTime = clock.getElapsedTime()
	
	object1.position.y = Math.sin(elapsedTime * 0.3) * 1.5
	object2.position.y = Math.sin(elapsedTime * 0.8) * 1.5
	object3.position.y = Math.sin(elapsedTime * 1.4) * 1.5
	
	const targets = [object1, object2, object3]
	raycaster.setFromCamera(mouseCoor, camera)
	const intersections = raycaster.intersectObjects(targets)

	// Detect Mouse enter and mouse leave
	if (intersections.length) {
	    if (witness == null) {
	        console.log("Mouse Enter")
	    }
	    witness = intersections[0]
	}
	else {
	    if (witness != null) {
	        console.log("Mouse leave")
	    }
	    witness = null
	}
}
```

We try to detect if the length of the intersections variable is not equal to 0 and if true, then we will detect it the witness variable is null then log Mouse Enter, we assign the witness variable an object, now it is not null, 
Else we will detect if the witness is not null then we will output mouse leave then set the witness again into null.



