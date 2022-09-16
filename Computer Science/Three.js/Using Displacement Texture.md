# Displacement Texture
[[Displacement Texture]] or height texture modifues how much will the [[Three.js Geometry|geometry]] will become displaced.
![[Pasted image 20220811133017.png]]


The dark spot will do doesn, the white will do up and the grey will stay put. Using [[Standard Material]], we could do this
```js
const material = new THREE.MeshStandardMaterial()
material.side = THREE.DoubleSide;
material.metalness = 0;
material.roughness = 1;
material.map = colorTexture;
material.aoMap = ambientOcclusionTexture;
material.aoMapIntensity = 1;

material.displacementMap = heightTexture;
```

![[Pasted image 20220817055857.png]]

This is too much, to reduce the intensity of  the displacment. set the value into a float of 0.01, using `displacementScale`

```js
material.displacementScale = 0.01
```

