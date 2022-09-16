# Texture Loader
This method will allow you to load dfferent [[Three.js Textures]] a bunch of times
```js
const textureLoader = new THREE.TextureLoader()
```

After this, is we create another variable and use this object to load a texture, for instance, a [[Color Texture]].
```js
const texture = textureLoader.load("texture/door/color.jpg")
```

This have several  callbacks namely the loaded, progress and error callbacks which we could define like this
```js
const texture = textureLoader.load("texture/door/color.jpg", 
								   () => {console.log("Loaded")}, 
								   () => {console.log("Progress")}, 
								   () => {console.log("Error")})
```

To make this easier, we could just pass in a [[Three.js Loading Manager]]
```js
const textureLoader = new THREE.TextureLoader(loadingManager)
```

We could also load multiple texture at once
```js
const loadingManager = new THREE.LoadingManager(loadingManager);

const textureLoader = new THREE.TextureLoader(loadingManager)
const colorTexture = textureLoader.load("textures/door/color.jpg")
const alphaTexture = textureLoader.load("textures/door/alpha.jpg")
const ambientOcclusionTexture = textureLoader.load("textures/door/ambientOcclusion.jpg")
const heightTexture = textureLoader.load("textures/door/height.jpg")
const metalnessTexture = textureLoader.load("textures/door/metalness.jpg")
const normalTexture = textureLoader.load("textures/door/normal.jpg")
const roughnessTexture = textureLoader.load("textures/door/roughness.jpg")
```

![[Pasted image 20220816060248.png]]

