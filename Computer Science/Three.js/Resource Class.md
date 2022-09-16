# Resource Class
This will handle the [[Three.js Textures]] and [[Three.js Texture Loader]]

Import the necessary tools and the [[Event Trigger Class]] as well as [[GLTFLoader()]] and [[Three.js (core)]]
```js
import EventEmitter from "./EventEmitter";
import { GLTFLoader } from "three/examples/jsm/loaders/GLTFLoader"
import * as THREE from "three"
```

Create the class and extends the [[Event Trigger Class]]
```js
export default class Resources extends EventEmitter{
    constructor() {
		super()
    }
```

This must have a [[Source Class]] where we will store the textures
```js
export default class Resources extends EventEmitter{
    constructor(resource) {
        super()
        this.resource = resource
        this.item = {} // store the textures
        this.numberOfItems = this.resource.length // length of the array
        this.loaded = 0 // will be equal to the length if finished loading
    }
```

Create a method that will instantiate the loaders such as [[GLTFLoader()]], [[Three.js Cube Texture Loader]], [[Three.js Texture Loader]]
```js
instantiateLoader() {
    this.loader = {}
    this.loader.gltfLoader = new GLTFLoader()
    this.loader.cubeTextureLoader = new THREE.CubeTextureLoader()
    this.loader.textureLoader = new THREE.TextureLoader()
}
```

We will create another method that will go and traverse the sources.
The structure of the soruces is like this
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
    }
]
```

So the method loop must be like
```js
startLoader() {
	for(let resource of this.resource) {
		if(resource.type == "gltfResource") {
			this.loader.gltfLoader.load(
				resource.path,
				(file) => {
					console.log(resource, file)  // callback after completion
				}
			)
		}
		else if(resource.type == "texture") {
			this.loader.textureLoader.load(
				resource.path,
				(file) => {
					console.log(resource, file)  // callback after completion
				}
			)
		}
		else if(resource.type == "cubeTexture") {
			this.loader.cubeTextureLoader.load(
				resource.path,
				(file) => {
					console.log(resource, file)  // callback after completion
				}
			)
		}
	}
	
}
```

![[Pasted image 20220829165222.png]]


Now, we coul detect when the textures are finished loading using  a method
```js
sourceLoaded(resource, file) {
	// Store the item to the item object with the name from the resouce
	this.item[resource.name] = file
	// Increment the loaded attribute
	this.loaded = 0
	// If loaded is equal to length, it is finished loading
	if (this.loaded == this.numberOfItems) {
	    console.log("Finished Loading")
	    console.log(this.item)
	}
}
```

We use a trigger on this
```js

sourceLoaded(resource, file) {
	this.item[resource.name] = file
	this.loaded = 0
	if (this.loaded == this.numberOfItems) {
		this.trigger("ready")
	}
}
```

In the [[World Class]], we set the nstantiation of the [[Environment Class]] only when the texture are ready
```js
export default class World{
    constructor() {
        this.experience = new Experience()

		// Add resources
        this.resource = this.experience.resources
        this.scene = this.experience.scenery
        const test = new THREE.Mesh(
            new THREE.BoxBufferGeometry(1, 1, 1),
            new THREE.MeshStandardMaterial({})
        )
        this.scene.add(test)

		// Instantiate the Enviroment of the resource is ready
        this.resource.on("ready", () => {
            this.env = new Environment()
        })
    }
}
```

now into our [[Environment Class]], we will create a enviroment function that will create the environment
```js
export default class Environment{
    constructor() {
        this.experience = new Experience()
        this.scene = this.experience.scenery
        // Add resources
        this.resources = this.experience.resources
        this.setSunlight()
        this.setEnvironmentMap()
    }

    setSunlight() {
        this.sunlight = new THREE.DirectionalLight("#fff", 4)
        this.sunlight.castShadow = true
        this.sunlight.shadow.camera.far = 15
        this.sunlight.shadow.mapSize.set(1024, 1024)
        this.sunlight.shadow.normalBias = 0.05
        this.sunlight.position.set(3.5, 2, -1.25)
        this.scene.add(this.sunlight)
    }

	// Create environment
    setEnvironmentMap() {
	    // Storage
        this.environmentMap = {}
        this.environmentMap.intensity = 0.4

        this.environmentMap.texture = this.resources.items.environmentMapTexture
        this.environmentMap.texture.encoding = THREE.sRGBEncoding

        this.scene.environment = this.environmentMap.texture

    }

}
```

Some times, texture is applied before creating the geometry, what we could do is to manually apply the [[Using Environment Texture|env map]] through a loop.
When will create a function in the `this.environmentMap` , in this function, we will traverse the scene and update the env map like what we do to create a [[Realistic Rendering]]
```js
setEnvironmentMap() {
	// Storage
	this.environmentMap = {}
	this.environmentMap.intensity = 0.4

	this.environmentMap.texture = this.resources.items.environmentMapTexture
	this.environmentMap.texture.encoding = THREE.sRGBEncoding

	this.scene.environment = this.environmentMap.texture

	this.environmentMap.needsUpdate = () => {
		
	}
}
```

TRaverse all item in the scene, filter only the Mesh type and with material that is [[Standard Material]]
```js
setEnvironmentMap() {
	// Storage
	this.environmentMap = {}
	this.environmentMap.intensity = 0.4

	this.environmentMap.texture = this.resources.items.environmentMapTexture
	this.environmentMap.texture.encoding = THREE.sRGBEncoding

	this.scene.environment = this.environmentMap.texture

	this.environmentMap.needsUpdate = () => {
		this.scene.traverse((child) => {
			child.material.envMap = this.environmentMap.texture
			child.material.envMapIntensity = this.environmentMap.intensity
			child.material.needsUpdate = true
		})
	}

	// Call the method
	this.environmentMap.needsUpdate()
}
```


![[Pasted image 20220830052959.png]]


