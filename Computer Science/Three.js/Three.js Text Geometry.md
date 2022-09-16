# Text Geometry
In [[Three.js (core)]], it is already given that the text is a Buffer Geometry which logs the `isBufferGeometry` property to true and is found on the example modules. To use this we need first to import it from the example

```js
import { TextGeometry } from "three/examples/jsm/geometries/TextGeometry.js"
```

Next is to use the Font Loader Class
Is not part of the core library therefore we need to import it from the example, this will accepts a typeface.json file. 

To create a typeface.json from an ordinary font file, use this website from [gero3](https://gero3.github.io/facetype.js/).
Import the font loader

```js
import { FontLoader } from "three/examples/jsm/loaders/FontLoader.js"
```

This is like [[Three.js Texture Loader]] where we could call `load` method but it doesn't return a value but we need to provide a callback for it.

```js
const fontLoader = new THREE.FontLoader();
fontLoader.load()
```

The callback is the file path of the font and a callback in which we will create the actural [[Three.js Geometry|geometry]] and [[Three.js Materials|material]], assuming the font is in static folder. 

```js
fontLoader.load(
	"/fonts/helvetiker_regular.typeface.json", 
	(font) => {
		const textGeometry = new TextGeometry()
	})
```

The callback function creates a font parameter which is the actual font from the file path we provided
Text Geometry accepts 2 main parameters which is the text and the properties of the text such as height, sgments and bevel

```js
fontLoader.load(
	"/fonts/helvetiker_regular.typeface.json", 
	(font) => {
		const textGeometry = new TextGeometry(
		"Hello World", 
		{
			font: font,
			size: 0.4,
			height: 0.2,
			curveSegments: 12, 
			bevelEnabled: true, 
			bevelThickness: 0.03,
			bevelSize: 0.02,
			bevelOffset: 0,
			bevelSegments: 12
		})
	})
```

- font : the font 
- height: the height of the font
- size: the size of the font
- curve segment: the amount of detail in the curves
- bevelEnabled: whether to include a border like detail in the corner of the text
- bevelThickness
- bevelSize
- bevelSegments: the amount of detail of the bevel
- bevelOffset

NExt part is to create the materials and combine the [[Three.js Geometry|geometry]] and [[Three.js Materials|material]] to a [[Three.js Mesh|mesh]]

```js
fontLoader.load(
	"/fonts/helvetiker_regular.typeface.json", 
	(font) => {
		const textGeometry = new TextGeometry(
		"Hello World", 
		{
			font: font,
			size: 0.4,
			height: 0.2,
			curveSegments: 12, 
			bevelEnabled: true, 
			bevelThickness: 0.03,
			bevelSize: 0.02,
			bevelOffset: 0,
			bevelSegments: 12
		})
	})
	const textMaterial = new THREE.MeshBasicMaterial();
	const text =  new THREE.Mesh(textGeometry, textMaterial);
	scene.add(text);
)
```

![[Pasted image 20220817112051.png]]

The problem is, it is hard for the [[GPU]] to handle such detailed text. If we enable the wireframe in the [[Basic Material]]![[Pasted image 20220817112224.png]]

We could see that there are too much detail and this will slow our device, we need to optimize and lessen the `curveSegments` and `bevelSegments`

```js
fontLoader.load(
	"/fonts/helvetiker_regular.typeface.json", 
	(font) => {
		const textGeometry = new TextGeometry(
		"Hello World", 
		{
			font: font,
			size: 0.4,
			height: 0.2,
			curveSegments: 5, 
			bevelEnabled: true, 
			bevelThickness: 0.03,
			bevelSize: 0.02,
			bevelOffset: 0,
			bevelSegments: 4
		})
	})
	const textMaterial = new THREE.MeshBasicMaterial();
	const text =  new THREE.Mesh(textGeometry, textMaterial);
	scene.add(text);
```

![[Pasted image 20220817112417.png]]

We avoid using text as much as possible. 
Now, we consider [[Centering Three.js Meshes]]
