# Floor Class
Create a class with imported [[Three.js Scene|scene]] and the [[Resource Class]]

```js
export default class Floor{
	constructor() {
	    this.experience = new Experience()
	    this.scene = this.experience.scenery
	    this.resource = this.experience.resources
  
	    this.setGeometry()
	    this.setTexture()
	    this.setMaterial()
	    this.setMesh()
}
```

This will have 4 methods as seen above, each wil handle eacj own thing
The geometry method will handle the geometry 
```js
setGeometry() {
	this.geometry = new THREE.CircleBufferGeometry(5, 64)
}
```

The texture will load all the resource from the [[Resource Class]]
```js
setTexture() {
	this.textures = {}
	
	this.textures.color = this.resource.items.dirtColorTexture
	this.textures.color.encoding = THREE.sRGBEncoding
	this.textures.color.repeat.set(1.5, 1.5)
	this.textures.color.wrapS = THREE.RepeatWrapping
	this.textures.color.wrapT = THREE.RepeatWrapping

	this.textures.normal = this.resource.items.dirtNormalTexture
	this.textures.normal.repeat.set(1.5, 1.5)
	this.textures.normal.wrapS = THREE.RepeatWrapping
	this.textures.normal.wrapT = THREE.RepeatWrapping
}
```

This will have some [[Three.js Repeat Texture|RepeatWrapping]] and [[Realistic Rendering]]
Next is [[Three.js Materials|material]] method
```js
setMaterial() {
	this.material = new THREE.MeshStandardMaterial()
	this.material.map = this.textures.color
	this.material.normalMap = this.textures.normal
}
```

The [[Resource Class]] will have its [[Source Class]] like this
```js
export default [
    {
        name: "environmentMapTexture",
        type: "cubeTexture",
        path: [
            "/textures/environmentMap/px.jpg",
            "/textures/environmentMap/nx.jpg",
            "/textures/environmentMap/py.jpg",
            "/textures/environmentMap/ny.jpg",
            "/textures/environmentMap/pz.jpg",
            "/textures/environmentMap/nz.jpg",
        ]
    },
    {
        name: "dirtColorTexture",
        type: "texture",
        path: "/textures/dirt/color.jpg"
    },
    {
        name: "dirtNormalTexture",
        type: "texture",
        path: "/textures/dirt/normal.jpg"
    },
]
```

The [[Three.js Mesh|mesh]] method will have this.
```js
setMesh() {
    this.mesh = new THREE.Mesh(
        this.geometry,
        this.material
    )
        
    this.mesh.receiveShadow = true
    this.mesh.rotation.x = - Math.PI  * 0.5
    this.scene.add(this.mesh)
}
```

Also, in the [[World Class]], we will first call this floor class before the  [[Environment Class]]
```js
this.resource.on("ready", () => {
	this.floor = new Floor()
	this.env = new Environment()
})
```








