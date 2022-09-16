# Random Particles
![[chrome-capture-2022-7-19 (1).gif]]

First thing to do is to create a Buffer Geometry
```js
const particleGeometry = new THREE.BufferGeometry()
```

Next is to create a container array that will store the position of the random coordinates and then specify the amount of coordinates, if we have 500 particles, then we need 500 * 3 coordinates values
```js
const count = 500
const coordinates = new Float32Array(count * 3)
```

Create a random value and store it to the array using for loop
```js
for(let i = 0; i < count * 3; i++) {
	coordinates[i] = (Math.random() - 0.5) * 30
}
```

We want it to have negative values which is why we substract it by 0.5
Then we apply it to the position of particleGeometry
```js
particleGeometry.setAttributes(
	"position",
	new THREE.BufferAttribtues(coordinates, 3)
)
```

Now, we could set it to a [[Three,js Particles]] materials and mesh
```js
const particleMaterial = new THREE.PointsMaterial({
    size: 0.1,
    sizeAttenuation: true,
})

const sphereParticle = new THREE.Points(particleGeometry, particleMaterial)
scene.add(sphereParticle)
```



