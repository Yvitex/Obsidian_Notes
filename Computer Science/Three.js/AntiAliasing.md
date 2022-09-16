---
aliases: [multisampling, supersampling, FXAA, SMAA, SSAA, TAA]
---
# Anti Aliasing
## Three.js Antialiasing
![[Pasted image 20220826100332.png]]

Is the produciton of stair like effects on the side of the meshes because of how decision on the pixels work![[Pasted image 20220826100427.png]]

The image above represents how it occurs and to solve this problem, what we could do is to divide the pixel into a much smaller pixels.
we have 2 ways in doing so:
- Super Sampling or Full Sampling
- MultiSampling

Super sampling is less performant way of doing this as it subdivide all pixels into smaller pixels. 
Multi sampling only subdivide the edges.

To implement multisampling, just add the `antialias: true` in the instantiation of [[WebGL Renderer|renderer]]. Beware that iw will not work if we apply this after the instantiation
```js
const renderer = new THREE.WebGLRenderer({
  canvas: canvas,
  antialias: true
});
```

![[Pasted image 20220826100951.png]]

Only smaller portion is visible which is not a big of a deal anymore.

## After Using Effect Composer
After using the [[Three.js EffectComposer]], you might find some antialiasing in the model. We could use different solutions to solve this problem

The first and easiest solution is just to change the `WebGLRenderTarget` as `WebGLMultisampleRenderTarget`
```js
const renderTarget = new THREE.WebGLMultisampleRenderTarget(
    800, 600,
    {
        minFilter: THREE.LinearFilter,
        magFilter: THREE.LinearFilter,
        format: THREE.RGBFormat,
        encoding: THREE.sRGBEncoding,
    }
)
```
![[Pasted image 20220913033152.png]]

The problem is that this is already depricated, what we could do is to use the [[Three.js Post Processing]] passes to do this. We have different kinds of atialiases passes such as:
- FXAA - performant but blurry
- SMAA - Less performant but better than FXAA
- SSAA - Best quality but worst performance
- TAA - Performant but limited

Import one of them
```js
import {SMAAPass} from 'three/examples/jsm/postprocessing/SMAAPass'
```

Apply it to the [[Three.js EffectComposer]]
```js
const smaaFilter = new SMAAPass()
smaaFilter.enabled = true
composer.addPass(smaaFilter)
```

![[Pasted image 20220913033924.png]]

It;s now slightly better. But this is very less performant so try to avoid using it, Also, if the user's pixel ratio is above 1, then we don't need anti aliasing at all
```js
if(renderer.getPixelRatio() == 1) {
    const smaaFilter = new SMAAPass()
    smaaFilter.enabled = true
    composer.addPass(smaaFilter)
}
```

