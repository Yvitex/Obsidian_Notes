# Renderer Class
If we already make the instance of the [[Experience Class]] a 🛑singleton, then the first thing to do in this class is to get the [[Sizes Class]] , the canvas, and the [[Camera Class]] and the [[Three.js Scene|scene]]
```js
import Experience from "../Experience.js"

export default class Renderer{
	constructor() {
		this.experience = new Experience()
		this.size = this.experience.size
		this.canvas = this.experience.canvas
		this.scene = this.experience.scene
		this.camera = this.camera
	}
}
```

Create a method that will create the instance of the [[WebGL Renderer]]
```js
setInstance() {
        this.instance = new THREE.WebGLRenderer({
            canvas: this.canvas,
            antialias: true
        })
		// Set the other properties
		this.instance.physicallyCorrectLights = true
        this.instance.outputEncoding = THREE.sRGBEncoding
        this.instance.toneMapping = THREE.CineonToneMapping
        this.instance.toneMappingExposure = 1.75
        this.instance.shadowMap.enabled = true
        this.instance.shadowMap.type = THREE.PCFShadowMap
        this.instance.setClearColor("#211d20")
}
```

We also need to set the size as well as the pixel ratio that could be found in the [[Sizes Class]]
```js
setInstance() {
        this.instance = new THREE.WebGLRenderer({
            canvas: this.canvas,
            antialias: true
        })
		this.instance.physicallyCorrectLights = true
        this.instance.outputEncoding = THREE.sRGBEncoding
        this.instance.toneMapping = THREE.CineonToneMapping
        this.instance.toneMappingExposure = 1.75
        this.instance.shadowMap.enabled = true
        this.instance.shadowMap.type = THREE.PCFShadowMap
        this.instance.setClearColor("#211d20")

		// Set Size
        this.instance.setSize(this.size.width, this.size.height)
        this.instance.setPixelRatio(this.size.pixelRatio)
}
```

What we want is that, when we update the size, the renderer will follow, create a method that will handle it 
```js
resize() {
	// We could just copy the set size method above
	this.instance.setSize(this.size.width, this.size.height)
	this.instance.setPixelRatio(this.size.pixelRatio)
}
```

We need to render it in each frame so we want this to be updating continuously, create an update method that will render each frame
```js
update() {
	this.instance.render(this.scene, this.camera.instance)
}
```

We use the instance property of the camera class, not the camera itself
Apply the instance method to the constructor
```js
import Experience from "../Experience.js"

export default class Renderer{
	constructor() {
		this.experience = new Experience()
		this.size = this.experience.size
		this.canvas = this.experience.canvas
		this.scene = this.experience.scene
		this.camera = this.camera
		this.setInstance()
	}
}
```

Inside the [[Experience Class]], we make the resize and update functional
```js
resize() {
    this.camera.resize()
    this.renderer.resize()
}

update() {
    this.camera.update()
    this.renderer.update()
}
```

[[Fullscreen Mode]]
