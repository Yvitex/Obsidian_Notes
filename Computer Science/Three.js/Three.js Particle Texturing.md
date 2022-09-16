# Particle Texturing
![[Pasted image 20220819142823.png]]

We could apply a texture to the [[Three,js Particles]] but as we could see, it will create an image instead that looks like a square. 
```js
const textureLoader = new THREE.TextureLoader()
const ring = textureLoader.load("/textures/particles/2.png")

const particleMaterial = new THREE.PointsMaterial({
    map: ring,
    size: 0.3,
    sizeAttenuation: true,
})

const sphereParticle = new THREE.Points(particleGeometry, particleMaterial)
scene.add(sphereParticle)
```

What we could do is transform this into an alpha map
```js
const textureLoader = new THREE.TextureLoader()
const ring = textureLoader.load("/textures/particles/2.png")

const particleMaterial = new THREE.PointsMaterial({
	transparent: true,
    alphaMap: ring,
    size: 0.3,
    sizeAttenuation: true,
})

const sphereParticle = new THREE.Points(particleGeometry, particleMaterial)
scene.add(sphereParticle)
```

![[Pasted image 20220819143140.png]]

Its well, still there are this black square that sometimes renders, sometimes, not. 
There are 3 solutions for this problem, first is by applu 0.01 to the `alphaTest` , alphaTest determines weather to render a mesg or not depending on its transparency.
```js
const particleMaterial = new THREE.PointsMaterial({
	color: "#ff88cc",
	transparent: true,
    alphaMap: ring,
    size: 0.3,
    sizeAttenuation: true,
    alphaTest: 0.01,
})
```

![[Pasted image 20220819143557.png]]


But there are still some dark sides around the circle. The next solution is using `depthTest`
```js
const particleMaterial = new THREE.PointsMaterial({
	color: "#ff88cc",
	transparent: true,
    alphaMap: ring,
    size: 0.3,
    sizeAttenuation: true,
    depthTest: false,
})
```

![[Pasted image 20220819143851.png]]

What this will do is that it will render everything, whether if the object is in the front of another object or not. The problem is if we create another mesh, we could see through that mesh and see the particles behind it. So don't use this.

The next solution is by turning `depthWrite` into false. This will disable the depth Buffer where we store what object is already rendered. 
```js
const particleMaterial = new THREE.PointsMaterial({
	color: "#ff88cc",
	transparent: true,
    alphaMap: ring,
    size: 0.3,
    sizeAttenuation: true,
    depthWrite: false,
})
```

![[Pasted image 20220819144049.png]]

we could change the color of the following to random colors. First is to set the `blending` property of the material to `THREE.AdditiveBlending`
```js
const particleMaterial = new THREE.PointsMaterial({
	color: "#ff88cc",
	transparent: true,
    alphaMap: ring,
    size: 0.3,
    sizeAttenuation: true,
    depthWrite: false,
})

particleMaterial.blending = THREE.AdditiveBlending
```

In the [[Three.js Random Particles]] construction part, add color arrays and set them to random values
```js
const particleGeometry = new THREE.BufferGeometry();
const numbers = 2000;
const coordinates = new Float32Array(numbers * 3);
const colors = new Float32Array(numbers * 3)

for (let i = 0; i < numbers * 3; i++) {
    coordinates[i] = (Math.random() - 0.5) * 30
    colors[i] = Math.random()
}
```

Then set it to an attribute with a name of colors in the geometry
```js
const particleGeometry = new THREE.BufferGeometry();
const numbers = 2000;
const coordinates = new Float32Array(numbers * 3);
const colors = new Float32Array(numbers * 3)

for (let i = 0; i < numbers * 3; i++) {
    coordinates[i] = (Math.random() - 0.5) * 30
    colors[i] = Math.random()
}

particleGeometry.setAttribute(
    "position",
    new THREE.BufferAttribute(coordinates, 3)
)

particleGeometry.setAttribute(
    "color",
    new THREE.BufferAttribute(colors, 3)
)
```

Then enable the `vertexColors`
```js
const particleMaterial = new THREE.PointsMaterial({
	color: "#ff88cc",
	transparent: true,
    alphaMap: ring,
    size: 0.3,
    sizeAttenuation: true,
    depthWrite: false,
    vertexColors: true,
})
```

![[Pasted image 20220819150716.png]]

