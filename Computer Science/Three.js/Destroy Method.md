# Destroy method
We destroy the following in order
- Events
- Geometry
- Materials

This will be written into the `destroy()` method at the [[Experience Class]]
```js
destroy() {
	this.size.off("resize")
	this.time.off("tick")
}
```

This is a method from [[Event Trigger Class]] that will stop listening to the resize or tick event from the [[Sizes Class]] and [[Time Class]]

Now we shall deestroy every geometry of [[Three.js Mesh|mesh]] using traverse
```js
destroy() {
	this.size.off("resize")
	this.time.off("tick")

	this.scene.traverse((child) => {
		child.geometry.dispose()
	})
}
```

Next is to traverse the material and find everything that could be disposed
```js
destroy() {
	this.size.off("resize")
	this.time.off("tick")

	this.scene.traverse((child) => {
		child.geometry.dispose()

		for(const key in child.material){
			const value = child.material[key] // get the value
			if (value && typeof value.dispose == "function") { // check if the dispose is a function
				value.dipose() //dispose it
			}
		}
	})
}
```

Next is to destroy the camera and renderer. we cant destroy the camera but we could destroy the [[Orbit Controls]]
```js
destroy() {
	this.size.off("resize")
	this.time.off("tick")

	this.scene.traverse((child) => {
		child.geometry.dispose()

		for(const key in child.material){
			const value = child.material[key] // get the value
			if (value && typeof value.dispose == "function") { // check if the dispose is a function
				value.dipose() //dispose it
			}
		}
	})
	this.camera.orbitControl.dispose()
	this.renderer.instance.dispose()
}
```