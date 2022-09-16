# Loading Manger
This is used to trigger callbacks and ensure how the back end is doing
```js
const loadingManager = new THREE.LoadingManager()
```

Use this instance to call the callbacks, onStart, onLoad, onProgress, onError
```js
loadingManager.onStart = () => {
	console.log("onStart")
}

loadingManager.onLoad = () => {
    console.log("onLoad")
}

loadingManager.onProgress = () => {
    console.log("onProgress")
}

loadingManager.onError = () => {
    console.log("onError")
}
```

This instance will be passed then when creating a [[Three.js Texture Loader]]
```js
const textureLoader = new THREE.TextureLoader(loadingManger)
```