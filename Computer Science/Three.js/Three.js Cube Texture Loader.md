# Cube texture Loader
Is the same as [[Three.js Texture Loader]] but for cube like textures forming a surrounging such as [[Using Environment Texture|environment texture]]

To do this, we instantitate the `CubeTextureLoader()` class
```js 
const cubeTextureLoader = new THREE.CubeTextureLoader();
```

Use the method `load` to create another variable that will hold the cube texture. This will accept an array of string of file location in this order (positive x, negative x, positive y, negative y, positive z then negative z)

```js
const environmentTexture = cubeTextureLoader.load([
  "/textures/environmentMaps/0/px.jpg",
  "/textures/environmentMaps/0/nx.jpg",
  "/textures/environmentMaps/0/py.jpg",
  "/textures/environmentMaps/0/ny.jpg",
  "/textures/environmentMaps/0/pz.jpg",
  "/textures/environmentMaps/0/nz.jpg"
]);
```

![[Pasted image 20220817083854.png]]

remember that the images must be a cube. We could download the environment texture from [Polyhaven](https://polyhaven.com/) which delivers high resolution HDRI or high dynamic range image for free. 
![[Pasted image 20220817084127.png]]

Then convert this images into cube form using this github website by [matheowis](https://matheowis.github.io/HDRI-to-CubeMap/)
