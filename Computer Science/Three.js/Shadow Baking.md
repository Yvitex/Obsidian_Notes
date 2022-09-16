# Shadow Baking
Here we use a[[Color Texture]]
![[bakedShadow.jpg]]

Is simply applying a [[Three.js Textures]] that have a built in shadow applied. We do not need to cast an actual [[Three,js Shadow]]

use the [[Three.js Texture Loader]]
```js
const textureLoader = new THREE.TextureLoader();
const bakedShadow = textureLoader("shadow.jpg")
```

Aply it to the mesh
```js
const planeWithShadow = new THREE.Mesh(new THREE.PlaneBufferGeometry, 
									  new THREE.MeshBasicMaterial({map: basedShadow}))
```

![[Pasted image 20220819045946.png]]

It looks cool. but it is not capable in animation and it has texture loader. 
We could use this other version I call [[Animated Shadow Bake]]
