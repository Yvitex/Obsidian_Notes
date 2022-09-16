# Click Event
We still use the old [[Three.js Click Event]]. 

```js
window.addEventListener("click", () => {
	
})
```

Using the animation code from [[Raycaster and MouseEvents]] section specially the witness variable.

```js
let witness = null
const tick = () =>

{
	const elapsedTime = clock.getElapsedTime()
	
	object1.position.y = Math.sin(elapsedTime * 0.3) * 1.5
	object2.position.y = Math.sin(elapsedTime * 0.8) * 1.5
	object3.position.y = Math.sin(elapsedTime * 1.4) * 1.5
	
	const targets = [object1, object2, object3]
	raycaster.setFromCamera(mouseCoor, camera)
	const intersections = raycaster.intersectObjects(targets)

	// Detect Mouse enter and mouse leave
	if (intersections.length) {
	    if (witness == null) {
	        console.log("Mouse Enter")
	    }
	    witness = intersections[0]
	}
	else {
	    if (witness != null) {
	        console.log("Mouse leave")
	    }
	    witness = null
	}
}
```

As we click, we are detecting if what we are clicking is an object inside the witness variable. Witness variable will be our reference that if there is an item isnide the witness variable, therefore the mouse clicking on a [[Three.js Mesh|mesh]]

```js
window.addEventListener("click", () => {
	// test if there is an item in the witness
	if (witness) {

		// if there is an otem in the witness as we click, set the color to green
		switch(witness.object) {
			case object1:
				object1.materials.color.set("#0f0")
				break
			case object2:
				object2.materials.color.set("#0f0")
				break
			case object3:
				object3.materials.color.set("#0f0")
				break

		}
	}
})
```

![[chrome-capture-2022-7-23 (2).gif]]



