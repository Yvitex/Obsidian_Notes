# Draco Loader
Draco compression models are low sized models that is need to be decompresed before using it. It is perfect to use for larger files or models that takes up too much space.

To do this, we first need to import the loader from the example three.js folder jsm
```js
import { DRACOLoader } from "three/examples/jsm/loaders/DRACOLoader"
```

Instantiate the loader
```js
const dracoLoader = new DRACOLoader()
```

The next step is to set up a decoder which is a worker in a different thread making it decompress faster, simply just copy the folder called draco from the node modules > three > examples > js > libs > draco, copy it inside the static folder
![[Pasted image 20220825094337.png]]

Set the path to the dracoLoader decoder
```js
dracoLoader.setDecoderPath("/draco/")
```

Then after that is to use the [[GLTFLoader()]] and set the `setDracoLoader` to the current dracoLoader
```js
gltfLoader.setDRACOLoader(dracoLoader)
```

Now, if we add it to the scene
```js
gltfLoader.load(
    "/models/Duck/glTF-Draco/Duck.gltf",
    (data) => {
        const items = [...data.scene.children]
        for (let children of items) {
            scene.add(children)
        }
    }
)
```

It will work

