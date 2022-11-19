---
aliases: []
---
# Import Baked Material to Three.js
To import the [[GLTF]] file to [[Three.js (core)]], what we could do is to use the [[GLTFLoader()]].
```js
const gltfLoader = new GLTFLoader()
gltfLoader.load(
	"portal.glb",
	(children) => {
		scene.add(children.scene)
	}
)
```

![[Pasted image 20220922050536.png]]

Currently, we can;t see it because we have'nt applied any material. Use a [[Basic Material]] for it just to test
```js
const bakedMaterial = new THREE.MeshBasicMaterial({color: "#ff0000"})
```

Apply it to the mesh using the `traverse()` method
```js
const gltfLoader = new GLTFLoader()
gltfLoader.load(
	"portal.glb",
	(children) => {
		children.scene.traverse(
			(child) => {
				child.material = bakedMaterial
			}
		)
		scene.add(children.scene)
	}
)
```

![[Pasted image 20220922050835.png]]

Use [[Three.js Texture Loader]] instead of colors 
```js
const textureLoader = new THREE.TextureLoader()
const bakedTexture = textureLoader.load("baked.jpg")

const bakedMaterial = new THREE.MeshBasicMaterial({map: bakedTexture})
```

![[Pasted image 20220922053226.png]]


Now the problem lies because of the orientation of blender to [[Three.js (core)]]. What we could do is to se the texture's property, `flipY` to false
```js
const textureLoader = new THREE.TextureLoader()
const bakedTexture = textureLoader.load("baked.jpg")

bakedTexture.flipY = false
```
![[Pasted image 20220922053504.png]]

Now, we need to correct the color for the better. We could correct it by setting the `sRGBEncoding` to the [[Three.js Textures]]'s  encoding and [[WebGL Renderer|renderer]]'s outputEncoding
```js
bakedTexture.encoding = THREE.sRGBEncoding
renderer.outputEncoding = THREE.sRGBEncoding
```

![[Pasted image 20220922053912.png]]

Notice the abberation in the portal and other emission material we exported, this has happened because we do not have done some [[UV Unwrapping]] for it. We must associate an individual [[Three.js Materials|material]] for it but the problem is, how can we choose that specific mesh? Using names. 

First of, edit the name in the blender software. We will change the portal light, and the pole lights
![[Pasted image 20220922060736.png]]

Export it once again and override the previous export. If we `console.log` the `resule.scene.children`, we could see an array of meshes with individual names, we could find our modified names in it
```js
gltfLoader.load(
	"portal.glb",
	(children) => {
		// Output arrays
		console.log(children.scene.children)
	
		children.scene.traverse(
			(child) => {
				child.material = bakedMaterial
			}
		)
		scene.add(children.scene)
	}
)
```

![[Pasted image 20220922061435.png]]

We could select this items using a [[Javascript Scpecial Operations]] called [[Javascript Scpecial Operations|find]].
```js
gltfLoader.load(
	"portal.glb",
	(children) => {

		const poleLightA = children.scene.children.find((result) => result == "poleLightA")
		const poleLightB = children.scene.children.find((result) => result == "poleLightB")
		const portalLight = children.scene.children.find((result) => result == "portalLight")
	
		children.scene.traverse(
			(child) => {
				child.material = bakedMaterial
			}
		)
		scene.add(children.scene)
	}
)
```

Create materials for them
```js
const poleMaterial = new THREE.MeshBasicMaterial({color: "#ffffe5"})
const portalMaterial = new THREE.MeshBasicMaterial({color: "#ffffff"})
```

Apply these materials
```js
gltfLoader.load(
	"portal.glb",
	(children) => {

		const poleLightA = children.scene.children.find((result) => result == "poleLightA")
		const poleLightB = children.scene.children.find((result) => result == "poleLightB")
		const portalLight = children.scene.children.find((result) => result == "portalLight")
	
		children.scene.traverse(
			(child) => {
				child.material = bakedMaterial
			}
		)

		// Apply Materials
		poleLightA.material = poleMaterial
		poleLightB.material = poleMaterial
		portalLight.material = portalMaterial

		scene.add(children.scene)
	}
)
```
![[Pasted image 20220922063335.png]]

### Optimization
If we test this out inside [[Spector.js]]. We would that there are so many render calls. 
![[Pasted image 20220923043922.png]]

Reduce it by merging all items exccept the lights inside blender. First, select all items except lights.
![[Pasted image 20220923044018.png]]

Next is to duplicate them by `shift + d`, don't move it rather, right mouse click. Press `ctrl + j`  to merge them into one geometry. Press `M` and put it inside a collection named Merge. Disable others except immersion mesh and merge collection

![[Pasted image 20220923044331.png]]

Actually, change the name into something that you like. I'll name it Mr.Merged. We could have removed all the materials applied in this mesh because in the end, we are exporting no materials but with [[Three.js Textures]] and UVs

![[Pasted image 20220923050357.png]]


We have reduced the render calls significantly. Now, to optimize it further, remembered that we set the texture for every child using the `traverse()` method? We could not set it only into 1 [[Three.js Mesh|mesh]] which means we do not need the traverse anymore but the [[Javascript Scpecial Operations]] called `find()`

```js
gltfLoader.load(
	"portal.glb",
	(children) => {

		const poleLightA = children.scene.children.find((result) => result.name == "poleLightA")
		const poleLightB = children.scene.children.find((result) => result.name == "poleLightB")
		const portalLight = children.scene.children.find((result) => result.name == "portalLight")
		const merged = children.scene.children.find((result) => result.name == "MrMerged")

		// Apply Materials
		poleLightA.material = poleMaterial
		poleLightB.material = poleMaterial
		portalLight.material = portalMaterial

		// Set the mesh with the material
		merged.material = bakedMaterial

		scene.add(children.scene)
	}
)
```

We could go then and [[Add More Details in Baked Material]]

# Metatags
###### Related: [[3D Baking]], [[GLTFLoader()]], [[Three.js Texture Loader]]
###### Tags: #three 
###### Source: 

---