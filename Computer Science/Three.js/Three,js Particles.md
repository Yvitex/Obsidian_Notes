# Particle
Small version of [[Three.js Mesh|mesh]] used for visual effects and animation
For starters we could trace a [[Three.js Geometry|geometry]] of a 3d object.
```js
const sphere = new THREE.SphereBufferGeometry(5, 25, 25);
```

Then create a material for those particles. Here ae are using `PointsMaterial()` constructor
```js
const particleMaterial = new THREE.PointsMaterial()
```

This will accept 2 attributes, namely size and `sizeAttenuation` or if we are reducing the size if the particle is far away.
```js
const particleMaterial = new THREE.PointsMaterial({
	size: 0.1,
	sizeAttenuation: true,
})
```

After that, create the mesh but this time, as a `Point` mesh
```js
const particle = new THREE.Points(sphere, particleMaterial);
scene.add(particle)
```

![[Pasted image 20220819134014.png]]


We could also apply some [[Three.js Textures]] to it. See, [[Three.js Particle Texturing]]

## Complex Topics
- [[Three.js Random Particles]]




## Resource
[Kenney.NL](https://www.kenney.nl/)
