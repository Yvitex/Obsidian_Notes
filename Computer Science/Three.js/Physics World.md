## Physics World
 
 Create a physics world, this would enable you to set the gravity intensity using 
 `gravity.set()` that accepts a vector 3 values, 
 
```js
const world = new CANNON.World()
world.gravity.set(0, -9.8, 0) 
```

Now create the shape of the object. we could use a sphere to match the shape of the 3d [[Three.js Mesh|mesh]]
```js
const physicsShape = new CANNON.Sphere(0.5)
```

Some of the shapes availble for us are:
- Box
- Cylinder
- Plane
- Sphere
- etc

`Sphere()` will accept a radius. In our case, the radius is equal to the radius of the mesh.
Now we could create the physicsBody that will make use of the shape
```js
const physicsBody = new CANNON.Body({
	mass: 1,
	position: new CANNON.Vec3(0, 3, 0), // set slightly above plane
	shape: physicsShape
})
```

The next step is to add it to the physics world
```js
world.addBody(physicsBody)
```

This will not yet work, we need to provide a setting for the world in order to update itself, inside our [[Three.js Animations]] tick function, we could make the world auto update each frame. but first we need to set the following in the `set` method of the world.

```js
const tick = () =>
{
    const elapsedTime = clock.getElapsedTime()
    
	// Set the world Step
    world.step() 

    // Update controls
    controls.update()

    // Render
    renderer.render(scene, camera)
    
    // Call tick again on the next frame
    window.requestAnimationFrame(tick)
}
```

tHIS WILL accept 3 parameters
- Fixed time set or frame rate
- Time passed after the last frame or [[Delta Time]]
- How many iteration to catch up from potential delay

```js
const clock = new THREE.Clock()
let previousFrame = 0

const tick = () =>
{
    const elapsedTime = clock.getElapsedTime()
    const deltaTime = elapsedTime - previousFrame
    previousFrame = elapsedTime

    world.step(1/60, deltaTime, 3)

    // Update controls
    controls.update()

    // Render
    renderer.render(scene, camera)

    // Call tick again on the next frame
    window.requestAnimationFrame(tick)
}
```

Now we could use the position of the physical body to reposition the [[Three.js Mesh|mesh]], we could simply copy the Vec3 to the three.js Vector3

```js
const clock = new THREE.Clock()
let previousFrame = 0

const tick = () =>
{
    const elapsedTime = clock.getElapsedTime()
    const deltaTime = elapsedTime - previousFrame
    previousFrame = elapsedTime

    world.step(1/60, deltaTime, 3)

	// Animation
	sphere.position.copy(physicalBody.position)

    // Update controls
    controls.update()

    // Render
    renderer.render(scene, camera)

    // Call tick again on the next frame
    window.requestAnimationFrame(tick)
}
```

![[chrome-capture-2022-7-24.gif]]

The problem is that the plane is not calculated by the library yet.
We need then to add the plane as a physical body

```js
const planeShape = new CANNON.Plane()
const physicalPlane = new CANNON.Body()
```

Set the mass to 0 if we want it to levitate and unbudge, 
```js
const planeShape = new CANNON.Plane()
const physicalPlane = new CANNON.Body()
physicalPlane.mass = 0
physicalPlane.addShape(planeShape)
world.addBody(physicalPlane)
```

The problem then it magically bounce because of wrong rotation axis

![[chrome-capture-2022-7-24 (1).gif]]

We need to rotate the plane, and to do this, is that we need to use [[Rotation (Three.js)|quarternion]], This is like [[Euler's Angle]] but with negative and positive orientation on axis

```js
physicalPlane.quaternion.setFromAxisAngle(
	new CANNON.Vec3(-1, 0, 0),
	Math.PI * 0.5
)
```

-1 as we need to rotate it from the negative  x axis. We could do positive too but it will have a different rotational direction. Then we rotate it a quarter of one revolution. 