## Environment Map Realistic Render
Apply [[Three.js Textures]] on the background using [[Three.js Cube Texture Loader]]
```js
const cubeLoader = new THREE.CubeTextureLoader()
const envTexture = cubeLoader.load(
   [ "/textures/environmentMaps/0/px.jpg",
    "/textures/environmentMaps/0/nx.jpg",
    "/textures/environmentMaps/0/py.jpg",
    "/textures/environmentMaps/0/ny.jpg",
    "/textures/environmentMaps/0/pz.jpg",
    "/textures/environmentMaps/0/nz.jpg",]
)
```


Apply this to the scene background
```js
scene.background = envTexture
```

![[Pasted image 20220826055353.png]]

The helmet doesn't match the light of the background, we must apply the environment texture to it and everything. Create a function for doing so.
First, execute the inexistent function isnide the [[GLTFLoader()]]
```js
const gltfLoader = new GLTFLoader();
gltfLoader.load("/models/FlightHelmet/glTF/FlightHelmet.gltf", (data) => {
  data.scene.scale.set(10, 10, 10);
  data.scene.rotation.y = Math.PI * 0.5;
  data.scene.position.y = -4;
  gui
    .add(data.scene.rotation, "y")
    .min(-Math.PI)
    .max(Math.PI)
    .step(0.001)
    .name("rotation");
  scene.add(data.scene);
  envMapChild(); // the function is here
});
```

We could get all the child in the scene using `traverse` method
```js
const applyEnvMap = () => {
	child.traverse((child) => {
		console.log(child)
	})
}
```

![[Pasted image 20220826055741.png]]

But as we could see, their are too many irrelevant child, we must only get the meshes and the allowed material to have envmap is the [[Standard Material]]. Use the `instanceof` for [[Javascript]]

```js
const envMapChild = () => {
  scene.traverse((child) => {
    if (
      child instanceof THREE.Mesh &&
      child.material instanceof THREE.MeshStandardMaterial
    ) {
      child.material.envMap = envTexture; // apply environment texture
      child.material.envMapIntensity = parameters.envIntensity; // value is 5
    }
  });
};
```

![[Pasted image 20220826060130.png]]



Or else, for simplicity, we could just add this code
```js
scene.environment =  envTexture
```


