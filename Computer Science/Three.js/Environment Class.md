# Environment Class
Will handle the [[Three.js Light]] like [[Directional Light]]
Instantiate the [[Experience Class]] and the [[Three.js (core)]]
```js
import * as THREE from "three"
import Experience from "../Experience"
```

Create a class
```js
export default class Environment{
	constructor() {
		this.experience = new Experience()
		this.scene = this.experience.scene
	}
}
```

Create method that will create a [[Directional Light]], this will have [[Three,js Shadow]]
```js
export default class Environment{
	constructor() {
		this.experience = new Experience()
		this.scene = this.experience.scene
	}
	
    setSublight() {
        this.sunlight = new THREE.DirectionalLight("#fff", 4)
        this.sunlight.castShadow = true
        this.sunlight.shadow.camera.far = 15
        this.sunlight.shadow.mapSize.set(1024, 1024)
        this.sunlight.shadow.normalBias = 0.05
        this.sunlight.position.set(3.5, 2, -1.25)
        this.scene.add(this.sunlight) // add to scene
    }
}
```



