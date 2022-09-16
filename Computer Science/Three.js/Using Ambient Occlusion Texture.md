# Ambient Occlusion
How can we use [[Ambient Occlusion]] texture to the [[Three.js (core)]] code. 

![[Pasted image 20220816175316.png]]

First is we need to set a second set of UV array into the [[Three.js Mesh|mesh]]es
```js
plane.geometry.setAttribute("uv2", 
							new THREE.MeshAttribute(plane.geometry.setAttrubute.uv.array, 2))
```

What;s happening here is that we set a second attribute we named as uv2 which has the same attribute as the current [[Three.js Mesh|mesh]] which is an array of uv
If we do this console.log
```js
console.log(plane.geometry.attribute.uv.array)
```

![[Pasted image 20220816175619.png]]

After we do this
```js
sphere.geometry.setAttribute("uv2", new THREE.BufferAttribute(sphere.geometry.attributes.uv.array, 2))

plane.geometry.setAttribute("uv2", new THREE.BufferAttribute(plane.geometry.attributes.uv.array, 2))

tohrus.geometry.setAttribute("uv2", new THREE.BufferAttribute(tohrus.geometry.attributes.uv.array, 2))
```

Then we could set the [[Ambient Occlusion]] texture in a [[Standard Material]] 
```js
material.aoMap = ambientOcclusionTexture;
```

![[Pasted image 20220816175915.png]]

This texture is loaded with [[Three.js Texture Loader]]. We could set the intensity to any value we want
```js
material.aoMapIntensity = 50;
```

![[Pasted image 20220816175959.png]]

