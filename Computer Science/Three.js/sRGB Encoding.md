# sRGB Encoding
![[Pasted image 20220826060130.png]]

Another way we could improve this lighting is to change the encoding either to `sRGBEncoding` or [[Gamma Encoding]]
To do this, we just could set the [[WebGL Renderer|renderer]] to 
```js
renderer.outputEncoding = THREE.sRGBEncoding
```

![[Pasted image 20220826084120.png]]

Now it looks realistic enough.
![[Pasted image 20220826084144.png]]

what happening here is that we are compressing the values based on optical illusion from LinearEncoding which is the default encoding.
This makes it easier to perceive the changes of light, the inconsistency is just because of wrong encoding that other software, like blender uses the sRGB version.

We could also use srgb Encoding into the [[Environment Map Realistic Render|environment map]]
```js
envTexture.encoding = THREE.sRGBEncoding
```

![[Pasted image 20220826091354.png]]