---
aliases: [THREE.Raycaster()]
---
# Raycaster
Used to detect object infront of the player, kinda like [[Interaction System|line trace]] in a horrorgame. [[Three.js (core)]] also have a built in method for doing so called `Raycaster()`

Instantiate the class
```js
const raycaster = new THREE.Raycaster()
```

Specify an origin point
```js
const raycasterOrigin = new THREE.Vector3(-3, 0, 0)
```

Specify the distance of the ray
```js
const raycasterDistance = new THREE.Vector3(10, 0, 0)
raycasterDistance.normalize() // raycasterDistance is always needs to be normalized
```

Combien this to the `raycaster` instance property
```js
raycaster.set(raycasterOrigin, raycasterDistance)
```

To use this, call the method `intersectObjects()` or `intersectObject()`. In intersectObject(), it only accepts 1 parameters object that it will detect. So for instance that we have these obejcts![[Pasted image 20220822134500.png]]
We could do this
```js
const intersect = intersectObject(object1)
console.log(intersect)
```

![[Pasted image 20220822134525.png]]

It output that one.
If for multiple ones, use this with a parameter of arrays
```js
const intersects = intersectObjects([object1, object2, object3])
console.log(intersects)
```

![[Pasted image 20220822134611.png]]

Here are some useful properties we could find inside here
- `distance` - distance between the origin of the ray and the colluion point
- `face` - what face of geometry was hit by the ray
- faceIndex - index of that face
- `object` - what object is concened by the collision
- `point` - a vector3 of the exact position of the collision
- `uv` - uv coordinates in that geometry (2d)

To test our race caster, to an animated object, we must cast a ray for each frame 
So inside out tick function in [[Three.js Animations]]
```js
tick = () => {
	const elapsedTime = clock.getElapsedTime()
	controls.update()
	renderer.render(camera, scene)
	window.requestAnimationFrame(tick)
}
```

When animating an object like this
![[chrome-capture-2022-7-23.gif]]

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

Spawn a ray casting origin and direction inside the tick function and test the objects
```js
tick = () => {
	const elapsedTime = clock.getElapsedTime()

	// Animation
    object1.position.y = Math.sin(elapsedTime * 0.3) * 1.5
    object2.position.y = Math.sin(elapsedTime * 0.8) * 1.5
    object3.position.y = Math.sin(elapsedTime * 1.4) * 1.5

	// Cast a ray
	const casterOrigin = new THREE.Vector3(-3, 0, 0)
	const casterDirection = new THREE.Vector3(1, 0, 0)
	casterDirection.normalize()
	raycaster.set(casterOrigin, casterDirection)

	// Test Intersection
	const test = [object1, object2, object3]
	const intersect = raycaster.intersectObjects(test)
	console.log(intersect.length)
    
	controls.update()
	renderer.render(camera, scene)
	window.requestAnimationFrame(tick)
```

![[Pasted image 20220823030753.png]]

This are the output which is the length of the array object intersecting with the raycaster. Sometimes it hits all three, sometimes it does not and only hits 2 or 1 and maybe none at all. Testing for each =frame might be too heavy for the browser, 

We could output the object property to modify some material properties of the intersected object, we could use for loop for this.

```js
tick = () => {
	const elapsedTime = clock.getElapsedTime()

	// Animation
    object1.position.y = Math.sin(elapsedTime * 0.3) * 1.5
    object2.position.y = Math.sin(elapsedTime * 0.8) * 1.5
    object3.position.y = Math.sin(elapsedTime * 1.4) * 1.5

	// Cast a ray
	const casterOrigin = new THREE.Vector3(-3, 0, 0)
	const casterDirection = new THREE.Vector3(1, 0, 0)
	casterDirection.normalize()
	raycaster.set(casterOrigin, casterDirection)

	// Test Intersection
	const test = [object1, object2, object3]
	const intersect = raycaster.intersectObjects(test)

	// Loop
	for (const intersected for intersect) {
		console.log(intersected.object)
	}
    
	controls.update()
	renderer.render(camera, scene)
	window.requestAnimationFrame(tick)
```

We could change the color of the intersected object by accessing its material property
```js
tick = () => {
	const elapsedTime = clock.getElapsedTime()

	// Animation
    object1.position.y = Math.sin(elapsedTime * 0.3) * 1.5
    object2.position.y = Math.sin(elapsedTime * 0.8) * 1.5
    object3.position.y = Math.sin(elapsedTime * 1.4) * 1.5

	// Cast a ray
	const casterOrigin = new THREE.Vector3(-3, 0, 0)
	const casterDirection = new THREE.Vector3(1, 0, 0)
	casterDirection.normalize()
	raycaster.set(casterOrigin, casterDirection)

	// Test Intersection
	const test = [object1, object2, object3]
	const intersect = raycaster.intersectObjects(test)

	// Loop and change color to blue
	for (const intersected for intersect) {
		intersected.object.material.color.set("#00f")
	}
    
	controls.update()
	renderer.render(camera, scene)
	window.requestAnimationFrame(tick)
```

![[Pasted image 20220823052945.png]]

The problem here is that as soon as it intersects, all spheres will turn into blue and not return to red as soon as they leave the intersection, for that, we could create another forloop that will force the color to red
```js
tick = () => {
	const elapsedTime = clock.getElapsedTime()

	// Animation
    object1.position.y = Math.sin(elapsedTime * 0.3) * 1.5
    object2.position.y = Math.sin(elapsedTime * 0.8) * 1.5
    object3.position.y = Math.sin(elapsedTime * 1.4) * 1.5

	// Cast a ray
	const casterOrigin = new THREE.Vector3(-3, 0, 0)
	const casterDirection = new THREE.Vector3(1, 0, 0)
	casterDirection.normalize()
	raycaster.set(casterOrigin, casterDirection)

	// Test Intersection
	const test = [object1, object2, object3]
	const intersect = raycaster.intersectObjects(test)

	// Return to color red
	for (const target for targets) {
		target.material.color.set("#f00")
	}

	// Loop and change color to blue
	for (const intersected for intersect) {
		intersected.object.material.color.set("#00f")
	}
    
	controls.update()
	renderer.render(camera, scene)
	window.requestAnimationFrame(tick)
```

![[chrome-capture-2022-7-23 (1).gif]]


Ray caster is useful when the time to use mouseevent occurs such as mouse enter or mouse leave. [[Raycaster and MouseEvents]]
