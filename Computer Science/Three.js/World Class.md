# World Class
We need to get the [[Three.js Scene|scene]] from the [[Experience Class]] and [[Three.js (core)]]
```js
import * as THREE from "three"
import Experience from "../Experience"
```

Create a constructor to be instantiated, 
```js
export default class World{
	constructor() {
		this.experience = new Experience()
		this.scene = this.experience.scene
	}
}
```

Test by creating a box wireframe
```js
export default class World{
	constructor() {
		this.experience = new Experience()
		this.scene = this.experience.scene

		const test = new THREE.Mesh(
			new THREE.BoxBufferGeometry(1, 1, 1),
			new THREE.MeshBasicMaterial({wireframe: true})
		)
	}
}
```

