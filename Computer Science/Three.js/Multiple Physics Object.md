# Multiple Physics Object
To create some multiple physics object, create a function that will do it
```js
const createSphere = (radius, position) => {
	// Create Mesh
	const mesh = new THREE.Mesh(
		new THREE.SphereBufferGeometry(radius, 20, 20),
        new THREE.MeshStandardMaterial({
            metalness: 0.3,
            roughness: 0.4,
            envMap: environmentMapTexture
        })
	)

	// Create Physics
	const shape = new CANNON.Sphere(radius)
	const body = new CANNON.Body({
		shape: shape,
		position: position,
		material: contactMaterial,
		mass: 1
	})

	world.addBody(body)
}

createSphere(1, {x: 0, y: 3, z: 0})
```

If we call the function, it will give us this![[Pasted image 20220824124057.png]]

It will not fall down because we are not updating its position, what we could do is to create an object data structure that will store the mesh and physics body reference
```js
const toUpdate = [] // create array

const createSphere = (radius, position) => {
	const mesh = new THREE.Mesh(
		new THREE.SphereBufferGeometry(radius, 20, 20),
        new THREE.MeshStandardMaterial({
            metalness: 0.3,
            roughness: 0.4,
            envMap: environmentMapTexture
        })
	)

	const shape = new CANNON.Sphere(radius)
	const body = new CANNON.Body({
		shape: shape,
		position: position,
		material: contactMaterial,
		mass: 1
	})

	world.addBody(body)

	toUpdate.push({ // store the mesh and body variable to array
		mesh: mesh,
		body: body,
	})
}

createSphere(1, {x: 0, y: 3, z: 0})
```

Inside the tick, update the meshes inside the array with the physics body position
```js
const tick = () =>
{
    const elapsedTime = clock.getElapsedTime()
    const deltaTime = elapsedTime - previousFrame
    previousFrame = elapsedTime
    world.step(1/60, deltaTime, 3)

    // Update Physics
    for (let update of toUpdateArray) {
        update.mesh.position.copy(update.body.position)
    }

    controls.update()

    renderer.render(scene, camera)

    window.requestAnimationFrame(tick)
}
```

We could add it into a gui like this
```js
const gui = new dat.GUI()

const parameters = {}
parameters.createSphere = () => {
    createSphere(
        Math.random() * 0.5,
        {
            x: (Math.random() - 0.5) * 5,
            y: 3,
            z: (Math.random() - 0.5) * 5,
        }
    )
}

gui.add(parameters, "createSphere")
```

We just randomized the coordinates and the size

```ad-Danger
title: Ive created a random box creator but it looks shit
collapse: open
The main problem is... It doesn't rotate!!!

```

For boxes, or a different shape, we must note that we must note that 
![[Pasted image 20220824161005.png]]

they have rotation, which we must update in the tick function
```js
const tick = () =>
{
    const elapsedTime = clock.getElapsedTime()
    const deltaTime = elapsedTime - previousFrame
    previousFrame = elapsedTime

    world.step(1/60, deltaTime, 3)
  
    // Update Physics and rotation
    for (let update of toUpdateArray) {
        update.mesh.position.copy(update.body.position)
        update.mesh.quaternion.copy(update.body.quaternion)
    }

    controls.update()
    renderer.render(scene, camera)
    window.requestAn
```

![[chrome-capture-2022-7-24 (4).gif]]


Also you might envounter a problem in creating a box physics, the shape contains a halfExtents which mean we must provide a Cannon vector3. We divide it by 2 because the width of the mesh is equal to width / 2 as the half extent is only half of that extent
```js
const boxMesh = new THREE.BoxBufferGeometry(1, 1, 1, 10, 10)
const createBox = (length, width, depth, position) => {
    // Mesh
    const mesh = new THREE.Mesh(
        boxMesh,
        sphereMaterial
    )
    mesh.position.copy(position)
    mesh.scale.x = length
    mesh.scale.y = width
    mesh.scale.z = depth
    mesh.castShadow = true
    scene.add(mesh)

    // Physics
    const shape = new CANNON.Box(new CANNON.Vec3(length / 2, width / 2, depth / 2))
    const body = new CANNON.Body({
        mass: 1,
        position: position,
        material: defaultContactMaterial,
        shape: shape
    })
    world.addBody(body)
    toUpdateArray.push({
        mesh: mesh,
        body: body
    })
}
```

