In order to import gltf models, we could use the GLTFLoader()
```js
import {GLTFLoader} from "three/examples/jsm/loaders/GLTFLoader"
```

Then we could now import the model by instantiating a loader hen using the `load` function to import the mesh
```js
const gltfLoader = new GLTFLoader()
const duckMesh = gltfLoader.load("/models/Duck/glTF/Duck.gltf",
									() => {
									console.log("success")
								    },
									() => {
									console.log("progress")
									},
									() => {
									console.log("error")}
									)
```

Here, we only imported the default [[GLTF]] model. The callbacks outputs success
![[Pasted image 20220825083035.png]]

We could do it like this witht he callbacks. Data will output some information about the mesh. 
```js
const duckMesh = gltfLoader.load(
    "/models/Duck/glTF/Duck.gltf",
    (data) => {
        console.log(data)
    }
)
```
![[Pasted image 20220825083317.png]]

The mesh is inside the `scene > children > object3d > children > mesh`. But we must also notce that the precise scale, rotation and position fo the material is stored outside of the [[Three.js Mesh|mesh]] in the `scene > children > object3d `

We also have 2 kinds of scene, one is singular, one is an array. 

To import the mesh, we have many ways like importing the whole scene, or importing the whole children, though some unncessary items might be included.

This is how you import by importing the whole children but with unnecessary camera
```js
const duckMesh = gltfLoader.load(
    "/models/Duck/glTF/Duck.gltf",
    (data) => {
        scene.add(data.scene.children[0])
    }
)
```

This will also work in binary files. 
![[Pasted image 20220825085343.png]]

For a more complex models, they might be composed of multiple childrens, which is we require to create a while loop. While loop and not for loop as items are automatically remove from the data as soon as it is imported to the scene, there fore using while loop we could pick the first one again and again until the array is empty

If we only do it like this
```js
const gltfLoader = new GLTFLoader()
gltfLoader.load(
    "/models/FlightHelmet/glTF/FlightHelmet.gltf",
    (data) => {
        scene.add(data.scene.children[0])
    }
)
```

![[Pasted image 20220825085714.png]]

It does not import everything at all
```js
const gltfLoader = new GLTFLoader()
gltfLoader.load(
    "/models/FlightHelmet/glTF/FlightHelmet.gltf",
    (data) => {
        while (data.scene.children.length) {
            scene.add(data.scene.children[0])
        }
    }
)
```

![[Pasted image 20220825085825.png]]

Or else, we could also use this
```js
gltfLoader.load(
    "/models/FlightHelmet/glTF/FlightHelmet.gltf",
    (data) => {
        const items = [...data.scene.children]
        for (let children of items) {
            scene.add(children)
        }
    }
)
```





