# Animating Particles
[[Three,js Particles]] are hard to do [[Three.js Animations]], the best way to do this is to create our own shader.

Inside the tick funciton
```js
const tick = () =>
{
    const elapsedTime = clock.getElapsedTime()
   
    // Update controls
    controls.update()
    // Render
    renderer.render(scene, camera)
    // Call tick again on the next frame
    window.requestAnimationFrame(tick)
}
tick()
```

What we could do is to access the items in the attribute position of the particle geometry using a for loop

```js
const tick = () =>
{
    const elapsedTime = clock.getElapsedTime()

	for(let i = 0; i < numbers; i++) {
		const i3 = i * 3;
	}

    // Update controls
    controls.update()
    // Render
    renderer.render(scene, camera)
    // Call tick again on the next frame
    window.requestAnimationFrame(tick)
}
tick()
```

Note that numbers is the total number of particles. i3 will have a number from 0, then 3, then 9 and so on. We could use this to access the array position attribute by 3's

```js
const tick = () =>
{
    const elapsedTime = clock.getElapsedTime()

	for(let i = 0; i < numbers; i++) {
		const i3 = i * 3;
		particleGeometry.attributes.position.array[i3 + 1] = Math.sin(elapsedTime)
	}

    controls.update()
    renderer.render(scene, camera)
    window.requestAnimationFrame(tick)
}
tick()
```

i3 + 1 will access the y axes of each set of xyz in the array attributes.
What we need now is an offset, we could do this using the value of x from each array set
```js
const tick = () =>
{
    const elapsedTime = clock.getElapsedTime()

	for(let i = 0; i < numbers; i++) {
		const i3 = i * 3;
		const x = particleGeometry.attributes.position.array[i3]
		particleGeometry.attributes.position.array[i3 + 1] = Math.sin(elapsedTime + x)
	}

    controls.update()
    renderer.render(scene, camera)
    window.requestAnimationFrame(tick)
}
tick()
```

![[chrome-capture-2022-7-19 (2).gif]]

This will be a follish errand for us to do unless we have less particles. 