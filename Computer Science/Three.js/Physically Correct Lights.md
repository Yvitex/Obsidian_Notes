## Physically Correct Lights
We have here a [[Standard Material]] with some [[Directional Light]] with intensity of 1, the value of the light is different from other 3d software. Why? Because three js uses a arbitary values than physically realistic values. 
But we could change it to that by applying this to the [[WebGL Renderer|renderer]]
```js
renderer.physicallyCorrectLights = true
```

![[Pasted image 20220826045104.png]]

It became dimmer

Apply a complex [[Three.js Mesh|mesh]] using [[GLTFLoader()]]
```js
const gltfLoader = new GLTFLoader()
gltfLoader.load(
    "/models/FlightHelmet/glTF/FlightHelmet.gltf",
    (data) => {
        data.scene.scale.set(10, 10, 10)
        data.scene.rotation.y = Math.PI * 0.5
        data.scene.position.y = -4
        gui.add(data.scene.rotation, "y").min(-Math.PI).max(Math.PI).step(0.001).name("rotation")
        scene.add(data.scene)
    }
)
```

![[Pasted image 20220826052331.png]]