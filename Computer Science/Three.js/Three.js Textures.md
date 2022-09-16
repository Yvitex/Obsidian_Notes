# Textures
There are several kinds of texture present in [[Three.js (core)]]:
-[[Color Texture]]
- [[Alpha Texture]]
-  [[Displacement Texture]]
- [[Normal Texture]]
- [[Ambient Occlusion]]
- [[Metalness]]
- [[Roughness]]

To load a texture, we could simply use an image object, load the color image then use it as a texture
```js
const image = new Image()
```

This is the image.  Now, we'll go an [[Importing Image]] using this object
```js
const image = new Image()
image.src = "/textures/door/color.jpg"
```

Then after this, we'll create the texture out of this image after the image has been loaded
```js
const image = new Image()

image.onload = () => {
	const texture = new THREE.Texture(image)
}

image.src = "/textures/door/color.jpg"
```

This won't work as it is a local variable. We can't apply this to the [[Three.js Materials|materials]]. What we;ll do is to do this outside the brackets like this
```js
const image = new Image()
const texture = new THREE.Texture(image)

image.onload = () => {

}

image.src = "/textures/door/color.jpg"
```

Then update the texture inside the load event listener
```js
const image = new Image()
const texture = new THREE.Texture(image)

image.onload = () => {
	texture.needsUpdate = true
}

image.src = "/textures/door/color.jpg"
```

![[Pasted image 20220816052433.png]]


Alternatively we could use a [[Three.js Texture Loader]] for an easier workflow

We could transform this texture in how many ways we want, we could:
- [[Three.js Texture Rotation|Rotate]]
- [[Three.js Repeat Texture|Repeat]]
- [[Three.js Texture Offset|Move]]
