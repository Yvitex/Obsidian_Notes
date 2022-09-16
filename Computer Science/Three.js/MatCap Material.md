---
aliases: [THREE.MeshMatcapMaterial(), matcap]
---
# Matcap Material
Matcap basically looks like this. ![[1.png]]

A sphere with some shading and others that could be applied to a specified [[Three.js Geometry|geometry]].
![[Pasted image 20220816160646.png]]

To use this, we should instantiate the `MeshMatcapMaterial()` class
```js
const material = new THREE.MeshMatcapMaterial();
```

Using a [[Three.js Texture Loader]], create a texture importing this matcap files.
```js
const textureLoader = new Three.TextureLoader();
const matcapTexture = textureLoader.load("/1.png");

const material = new THREE.MeshMatcapMaterial();
```

Use the `matcap` attribute to feed the loaded texture to the material
```js
const textureLoader = new Three.TextureLoader();
const matcapTexture = textureLoader.load("/1.png");

const material = new THREE.MeshMatcapMaterial();
material.matcap = matcapTexture;
```

We could create this in 3d software. 