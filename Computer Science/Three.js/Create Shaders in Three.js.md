---
aliases: [ShaderMaterial(), RawShaderMaterial()]
---
# Shadres Three.js
Three js have a way to create custom shader. In fact, we could have 2 methods to replace our [[Three.js Materials|material]]
We have 2 methods we could use:
- `ShaderMaterial()` - have built in codes
- `RawShaderMaterial()` - build it from scratch


After creating the geometry
```js
const geometry = new THREE.PlaneGeometry(1, 1, 32, 32)
```

Well use Raw Shader
```js
const material = new THREE.RawShaderMaterial({
	vertexShader: ``,
	fragmentShader: ``,
})
```

This will have 2 required parameter which are the [[Vertex Shader]] and the [[Fragment Shader]]. 

Write the shader in [[GLSL]] format
```js'
const material = new THREE.RawShaderMaterial({
	vertexShader: `
	uniform mat4 projectionMatrix;
	uniform mat4 viewMatrix;
	uniform mat4 modelMatrix;

	attribute vec3 position;

	void main() {
		gl_Position = projectionMatrix * viewMatrix * modelMatrix * vec4(position, 1.0);
	}`,
	
	fragmentShader: `
	precision mediump float;

	void main() {
	    gl_FragColor = vec4(1.0, 0.0, 0.0, 1.0);
	}`,
})
```

We could separate this into different file with `glsl` extension
![[Pasted image 20220831093007.png]]

vertex.glsl will have
```glsl
uniform mat4 projectionMatrix;
uniform mat4 viewMatrix;
uniform mat4 modelMatrix;
  
attribute vec3 position;

void main() {
    gl_Position = projectionMatrix * viewMatrix * modelMatrix * vec4(position, 1.0);
}
```

fragment.glsl will have
```glsl
precision mediump float;
void main() {
    gl_FragColor = vec4(1.0, 0.0, 0.0, 1.0);
}
```

Then we import it like this to the main js file
```js
import testVertexShader from "./Shaders/Test/vertex.glsl"
import testFragmentShader from "./Shaders/Test/fragment.glsl"
```

This will cause an error to the webpack. in the bundler folder, we  will edit it to allow the [[Shader]] file
![[Pasted image 20220831093236.png]]

We will mod the `webpack.common.js`
```js
test: /\.(glsl|vs|fs|vert|frag)$/,
	exclude: /node_modules/,
	use: [
		"raw-loader"
	]
```

We add that to the code. Raw loader will enable you to import that code as a string

