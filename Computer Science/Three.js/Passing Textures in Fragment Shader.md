# Passing Textures in Fragment Shader
We could also pass some [[Three.js Textures]] using it
First is to import the [[Color Texture]] using [[Three.js Texture Loader]]
```js
const textureLoader = new THREE.TextureLoader()
const flagTexture = textureLoader.load("/textures/flag-french.jpg")
```

Next is to import it to the [[GLSL]] using the [[Create Shaders in Three.js|RawShaderMaterial()]]
```js
const material = new THREE.RawShaderMaterial({
	vertexShader: testVertexShader,
	fragmentShader: testFragmentShader,
	uniforms: {
		uFrequency: {value: new THREE.Vector2(10, 5)},
		uTime: {value: 0},
		uColor: {value: new THREE.Color("orange")},
		uTexture: {value: flagTexture}
	}
})
```

Inside our [[Fragment Shader GLSL]], we need to import it as [[Shader Uniform]] with a dataype of `sampler2D`
```glsl
precision mediump float;

uniform sampler2D uTexture;
void main() {

}
```

To make use of it, we need to use the `texture2D` method
```glsl
precision mediump float;

uniform sampler2D uTexture;
void main() {
	vec4 textures = texture2D(uTexture, ) // it neeeds 2 arguments
}
```

The second argument is the [[UV Unwrapping|uv]] of the mesh. And because the [[Fragment Shader GLSL]] can only import [[Shader Uniform]] and [[Shader Varying]], we can't pass any [[Shader Attributes]]

What we could do is to pass that [[Shader Attributes]] to the [[Vertex Shader]] then pass it to the [[Fragment Shader]] as a [[Shader Varying]]

Remember that in our [[Three.js Geometry|geometry]], we have a uv  coordinates, we use that to our [[Vertex Shader]]
```glsl
uniform mat4 projectionMatrix;
uniform mat4 viewMatrix;
uniform mat4 modelMatrix;

uniform vec2 uFrequency;
uniform float uTime;

attribute vec3 position;
attribute float aRandom;

// Pass the uv coordinates as vec2
attribute vec2 uv;

varying float vRandom;

// Create a varying data 
varying vec2 vUv;

void main() {
    vec4 modelPosition = modelMatrix * vec4(position, 1.0);
    modelPosition.z += sin(modelPosition.x * uFrequency.x - uTime) * 0.1;
    modelPosition.z += sin(modelPosition.y * uFrequency.y - uTime) * 0.1;
    vec4 viewPosition = viewMatrix * modelPosition;
    vec4 projectedPosition = projectionMatrix * viewPosition;

    gl_Position = projectedPosition;
    vRandom = aRandom;
    // Use the value from the uv coordinate to the varying variable
    vUv = uv;
}
```

Insdide the [[Fragment Shader GLSL]]
```glsl
precision mediump float;
uniform vec3 uColor;
uniform sampler2D uTexture;

varying vec2 vUv;

void main() {
    vec4 textures = texture2D(uTexture, vUv);
    gl_FragColor = textures;
}
```

Then if we want to apply shadow, we will modify our [[Vertex Shader GLSL]] slightly to have more control.
First is to create a [[Shader Varying]] as we will pass that value to the [[Fragment Shader GLSL]]
```glsl
// elevation that will store the calculated depth of z
varying float vElevation;

void main() {
	vec4 modelPosition = modelMatrix * vec4(position, 1.0);

	// elevation will store the calculated depth of x and y combined applied to z
    float elevation = sin(modelPosition.x * uFrequency.x - uTime) * 0.1;
    elevation += sin(modelPosition.y * uFrequency.y - uTime) * 0.1;
    
    modelPosition.z += elevation;
    vec4 viewPosition = viewMatrix * modelPosition;
    vec4 projectedPosition = projectionMatrix * viewPosition;

    gl_Position = projectedPosition;
    vRandom = aRandom;

    vElevation = elevation;
    vUv = uv;
}
```

Re assign the value of the colors in fragment shader using these by dividing it based on the value.
```glsl
precision mediump float;

uniform vec3 uColor;
uniform sampler2D uTexture;

varying vec2 vUv;
varying float vElevation;

void main() {
    vec4 textures = texture2D(uTexture, vUv);

	// Re assign the value of xyz (no alpha), mult by 2 to increase brightness and plus 0.5 so that there is no negative values causing extreme darkness
    textures.xyz *= vElevation * 2.0 + 0.5;
    gl_FragColor = textures;
}
```

![[Pasted image 20220901152645.png]]
