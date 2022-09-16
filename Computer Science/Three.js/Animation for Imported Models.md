# Imported Animation Model
To animate the models with animations that are builtin, we could first look at the data by console logging the 

```js
gltfLoader.load(
    "/models/Fox/glTF/Fox.gltf",
    (data) => {
        console.log(data)
    }
)
```

![[Pasted image 20220825101832.png]]

We could see we have 3 animationClips
![[Pasted image 20220825102004.png]]

To play this, we must first create a mixer, we could do this by using the core `AnimationMixer` and we will pass the scene to be animated
```js
const mixer = new THREE.AnimationMixer(data.scene)
```

Next is to use the method isndie the mixer called `clipAnimation()` in here we will pass which animation to play
```js 
const action = new THREE.clipAnimation(data.animation[0])
```

Then we could play it
```js
action.play()
```

But, it won't work just yet, we need to pass the mixer inside the tick function in order t update the frames, because our mixer variable is not a global scope, we pass it as a global scope outisde the bracket
```js
let mixer = null

gltfLoader.load(
    "/models/Fox/glTF/Fox.gltf",
    (data) => {
        console.log(data)
        mixer = new THREE.AnimationMixer(data.scene)
        const action = mixer.clipAction(data.animations[0])
        action.play()
        
        data.scene.scale.set(0.025, 0.025, 0.025)
        scene.add(data.scene)
    }
)
```

Inside the tick function, we update the mixer using the [[Delta Time]] as the reference
```js
const tick = () =>
{
    const elapsedTime = clock.getElapsedTime()
    const deltaTime = elapsedTime - previousTime
    previousTime = elapsedTime

    mixer.update(deltaTime)

    // Update controls
    controls.update()
    
    // Render
    renderer.render(scene, camera)

    // Call tick again on the next frame
    window.requestAnimationFrame(tick)
}
```

![[Pasted image 20220825102709.png]]

We will get this error, it is because the first and so on tick detects a null value. we must filter this out using if statement
```js
const tick = () =>
{
    const elapsedTime = clock.getElapsedTime()
    const deltaTime = elapsedTime - previousTime
    previousTime = elapsedTime

	if (mixerl != null) {
		mixer.update(deltaTime)
	}

    // Update controls
    controls.update()
    
    // Render
    renderer.render(scene, camera)

    // Call tick again on the next frame
    window.requestAnimationFrame(tick)
}
```

![[chrome-capture-2022-7-25.gif]]