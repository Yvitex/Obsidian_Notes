---
aliases: [basicMaterial.color, basicMaterial.wireframe, basicMaterial.map, basicMaterial.transparent, basicMaterial.opacity, basicMaterial.map, material.side]
---
# Basic Material 
To specify a color, we instantiate the **MeshBasicMaterial**

```js
const material = new THREE.MeshBasicMaterial({color: 'red'})
```

Or we could do it like this
```js
const material = new THREE.MeshBasicMaterial();
material.color = new THREE.Color("red")
```

Or like this
```js
const material = new THREE.MeshBasicMaterial();
material.color.set("red")
```

Parameters inside the Three.js class contains a js.object as we have many properties we could add. Colors can also be in [[Hexadecimal Notation]]

There are many other use of basic material object. Like applying [[Three.js Textures]] with [[Three.js Texture Loader]]
```js
const textureLoader = new THREE.TextureLoader();
const colorTexture = textureLoader.load("/something.jpg")

const material = new THREE.MeshBasicMaterial();
material.map(colorTexture)
```

We could also set i t as wireframe
```js
const material = new THREE.MeshBasicMaterial({color: "red"});
material.wireframe = true;
```
![[Pasted image 20220816124611.png]]

And we could also set this to transparent
```js
const material = new THREE.MeshBasicMaterial({color: "red"});
material.transparent = true;
material.opacity = 0.2;
```
![[Pasted image 20220816124746.png]]


We could also use alphaMap that will use the [[Alpha Texture]] (see [[Using Alpha Texture]]) to map what part to make transparent. Remember that opacity and aphamap needs the transparency to be set to true
```js
const material = new THREE.MeshBasicMaterial();
material.map = colorTexture;
material.transparent = true;
material.alphaMap = alphaTexture;
```

![[Pasted image 20220816125415.png]]

![[chrome-capture-2022-7-16.gif]]

As we could see, the door texture disappearwhen rotated to the backside, to enable 2 face texture on both side
```js
const material = new THREE.MeshBasicMaterial();
material.map = colorTexture;
material.transparent = true;
material.alphaMap = alphaTexture;

material.side = THREE.DoubleSide;
```

![[chrome-capture-2022-7-16 (1).gif]]