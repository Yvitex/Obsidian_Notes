# Fox Class
An example of how you will approach creating a [[Three.js Mesh|mesh]] in the scene
Import necessary imports
```js
import * as THREE from "three"
import Experience from "../Experience"
```

Create a class that will get the [[Time Class]], [[Resource Class]], and the [[Three.js Scene|scene]]
```js
export default class Fox{
	constructor() {
		this.experience = new Experience()
		this.scene = this.experience.scenery
		this.resource = this.experience.resources.items.foxModel
		this.time = this.experience.time
}
```

We will create 2 methods which will import the model to the scene and one that will handle the [[Three.js Animations]]

Import model
```js
setModel() {
	this.model = this.resource.scene
	this.model.scale.set(0.02, 0.02, 0.02)
	
	this.model.traverse((child) => {
	    child.castShadow = true
	}) // cast shadow

	this.scene.add(this.model)
}
```

Create the animation
```js
setAnimation() {
	this.animation = {}
	this.animation.mixer = new THREE.AnimationMixer(this.model)
	this.animation.action = this.animation.mixer.clipAction(this.resource.animations[0])
	this.animation.action.play()
}
```

This will not work yet, we need to update the mixer along with the delta time. To do that, we will cascade the tick from the [[Experience Class]] to the [[World Class]] then to the [[Model or Fox Class]]

In the experience class add this code to the `update()`
```js
update() {
	this.camera.update()
	this.world.update() // update world
	this.renderer.update()
}
```

IN the world class, create a method called `update()`, this will update the fox
```js
update() {
    if(this.fox) {
        this.fox.update()
    }
}
```

There, we will check first if the fox already exist.
Now, we will create the `update()` for fox, that will use the [[Delta Time]] from the [[Time Class]]
```js
update() {
		this.animation.mixer.update(this.time.delta * 0.001)
	}
}
```

We divide it by 1000 because the update works on seconds



