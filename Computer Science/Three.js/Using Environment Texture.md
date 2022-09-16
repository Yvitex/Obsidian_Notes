# Environment Texture
Environment texture is the texture of an environment that shows an image of the surooundings if the [[Three.js Materials|material]] is reflective like glass or mirror. 

We could do this usign [[Standard Material]] via `envMap` property combined with [[Three.js Cube Texture Loader]]

![[Pasted image 20220817083854.png]]

```js 
const cubeTextureLoader = new THREE.CubeTextureLoader();
const environmentTexture = cubeTextureLoader.load([
  "/textures/environmentMaps/0/px.jpg",
  "/textures/environmentMaps/0/nx.jpg",
  "/textures/environmentMaps/0/py.jpg",
  "/textures/environmentMaps/0/ny.jpg",
  "/textures/environmentMaps/0/pz.jpg",
  "/textures/environmentMaps/0/nz.jpg"
]);
```

Using standard material and enough confifuration between [[Roughness]] and [[Metalness]], we could see the effect clearly
```js
const material = new THREE.MeshStandardMaterial();
material.roughness = 0.7;
material.metalness = 1;
material.envMap = environmentTexture;
```

![[Pasted image 20220817084757.png]]