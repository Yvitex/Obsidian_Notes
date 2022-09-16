---
aliases: []
---
# EffectComposer
This is a way to add [[Three.js Post Processing]].

Import it from the jsm folder in three node module
```js
import {EffectComposer} from 'three/examples/jsm/postprocessing/EffectComposer'
```

Import the pass
```js
import {RenderPass} from 'three/examples/jsm/postprocessing/RenderPass'
```

Instantiate the effectComposer class, this will take the renderer
```js
const composer = new EffectComposer(renderer)
```

Set up the appropriate pixel ratio and size
```js
const composer = new EffectComposer(renderer)
composer.setPixelRatio(Math.min(window.devicePixelRatio, 2))
composer.setSize(sizes.width, sizes.height)
```

Next is to add the pass or effect, this will need the scene and the camera
```js
const renderPass = new RenderPass(scene, camera)
```

Now we integrate it with each other using the composer's `addPass` method
```js
composer.addPass(renderPass)
```

We use the effectCOmposer then inside the tick function and replace the [[WebGL Renderer|render]]
```js
const tick = () =>
{
    const elapsedTime = clock.getElapsedTime()

    // Update controls
    controls.update()

    // Replace Render
    composer.render()

    // Call tick again on the next frame
    window.requestAnimationFrame(tick)
}
```

Now we could apply some effects to the screen, the documentation where we could choose is [here](https://threejs.org/docs/index.html?q=post#examples/en/postprocessing/EffectComposer)
![[Pasted image 20220912054339.png]]


To apply this effect, import it from the example files
```js
import {DotScreenPass} from 'three/examples/jsm/postprocessing/DotScreenPass'
```

Instantiate then add it to the effectComposer as a pass
```js
const dotScreen = new DotScreenPass()
dotScreen.enabled = true
composer.addPass(dotScreen)
```

![[Pasted image 20220912055657.png]]


Some of these passes needs some extrawork to do, for example `RGBShiftShader`
```js
import {RGBShiftShader} from 'three/examples/jsm/shaders/RGBShiftShader'
```

What we need to do is to import the `ShaderPass` and use `RGBShiftShader` on it.
```js
import {ShaderPass} from 'three/examples/jsm/postprocessing/ShaderPass'
```

Instantiate it with`RGBShiftShader` as a parameter
```js
const shaderPass = new ShaderPass(RGBShiftShader)
shaderPass.enabled = true
composer.addPass(shaderPass)
```

![[Pasted image 20220913020817.png]]



If we try glitch effect
```js
import {GlitchPass} from 'three/examples/jsm/postprocessing/GlitchPass'
```

```js
const glitchPass = new GlitchPass()
glitchPass.enabled = true
composer.addPass(glitchPass)
```

![[Pasted image 20220912055924.png]]

It seems darker than the original but why? 
It is because when we are using pass, we are also removing the [[sRGB Encoding]] making this code useless
```js
renderer.outputEncoding = THREE.sRGBEncoding
```

What we coul do is to create our own [[Three.js Post Processing|render target]] with [[sRGB Encoding]] inside.
USe the `WebGlRenderTarget`
```js
const renderTarget = new THREE.WebGLRenderTarget(
	800, 600,
	{
		minFilter: THREE.LinearFilter,
		magFilter: THREE.LinearFilter,
		format: THREE.RGBFormat,
		encoding: THREE.sRGBEncoding
	}
)
```

![[Pasted image 20220913030142.png]]

If we try to largen the viewport, it will get blurry all of a sudden, it is because we aren't updating the size of the `effectComposer`. On the resize listener, add this
```js
window.addEventListener('resize', () =>
{
    // Update sizes
    sizes.width = window.innerWidth
    sizes.height = window.innerHeight

    // Update camera
    camera.aspect = sizes.width / sizes.height
    camera.updateProjectionMatrix()

    // Update renderer
    renderer.setSize(sizes.width, sizes.height)
    renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2))

    composer.setPixelRatio(Math.min(window.devicePixelRatio, 2))
    composer.setSize(sizes.width, sizes.height)
})
```

We could use now other passes better like UnrealBloomPass and tweak it using [[Debug GUI]] or [[Custom Passes in Three.js]]
![[Pasted image 20220913041852.png]]


The problem now is their [[AntiAliasing]].