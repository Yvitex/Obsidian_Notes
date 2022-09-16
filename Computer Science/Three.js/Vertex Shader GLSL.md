# Vertex Shader GLSL
This is written in [[GLSL]] for [[Vertex Shader]]
```glsl
uniform mat4 projectionMatrix;
uniform mat4 viewMatrix;
uniform mat4 modelMatrix;
  
attribute vec3 position;

void main() {
    gl_Position = projectionMatrix * viewMatrix * modelMatrix * vec4(position, 1.0);
}
```

Remember that the main method is executed at run

![[Pasted image 20220831104102.png]]

We could move it by adding this code inside the main method.
```js
gl_Position.x += 0.5;
```
![[Pasted image 20220831104158.png]]

`gl_Position` is already defined from the start and we just need to override it. 
The long computation above
```js
gl_Position = projectionMatrix * viewMatrix * modelMatrix * vec4(position, 1.0);
```

Will handle the position of the vertices, and it will return a Vec(4).
```ad-Danger
title: Why Vec4 tho?
collapse: open
We need 4 values, the 3 is a vec3 of x y and z while the last one is the perspective ([[Homogenous Coordinates]]). This will create not a 2d environment but a clip space
```

![[Pasted image 20220831104955.png]]

Clip area is represented as the box

`modelMatrix` will determine the transformaiton of the [[Three.js Mesh|mesh]] along with vec4() position. (position, rotation, scale)

`viewMatrix` will determine the transformation of the [[Three.js Camera|camera]] (position, rotation, [[Field of View]], near, far)

`projectionMatrix` will determine the transformation of the clipArea. 

Take note that is is not built in glsl code but rather a [[Three.js (core)]] code.
We could separate this into 3 different variables for high control
```js
uniform mat4 projectionMatrix;
uniform mat4 viewMatrix;
uniform mat4 modelMatrix;

attribute vec3 position; // position attributes of x y z

void main() {
    vec4 modelPosition = modelMatrix * vec4(position, 1.0); // mesh

    vec4 viewPosition = viewMatrix * modelPosition;  // camera p
    vec4 projectedPosition = projectionMatrix * viewPosition; // clipArea

    gl_Position = projectedPosition;
}
```

Now we could add some calculation to make the plane became wave like using [[Trigonometric functions]]
```glsl
void main() {
    vec4 modelPosition = modelMatrix * vec4(position, 1.0); // mesh
	modelPosition.z += sin(modelPosition.x * 10) * 0.1
    vec4 viewPosition = viewMatrix * modelPosition;  // camera p
    vec4 projectedPosition = projectionMatrix * viewPosition; // clipArea

    gl_Position = projectedPosition;
}
```

![[Pasted image 20220831162810.png]]


We could create our own custom [[Shader Uniform]] value from the main javascript to the [[GLSL]].

So in our  [[Create Shaders in Three.js|RawShaderMaterial()]]m we could create another property called uniforms that will have an object
```js
const material = new THREE.RawShaderMaterial({
    vertexShader: testVertexShader,
    fragmentShader: testFragmentShader,
    uniforms: {
        uFrequency: {value: 10}
    }
})
```

We could pass it inside the [[Vertex Shader GLSL]] by adding a uniform variable similar to what we do in the 3 mat4 properties
```glsl
uniform mat4 projectionMatrix;
uniform mat4 viewMatrix;
uniform mat4 modelMatrix;

// Assign a variable
uniform float uFrequency;

attribute vec3 position;

void main() {
    vec4 modelPosition = modelMatrix * vec4(position, 1.0);
    
    // Set the variable
    modelPosition.z += sin(modelPosition.x * uFrequency) * 0.1;
    vec4 viewPosition = viewMatrix * modelPosition;
    vec4 projectedPosition = projectionMatrix * viewPosition;
    
    gl_Position = projectedPosition;
}
```

We could also make it looks like a flag that is animated, First is to make the u frequency as vector 2 with x and y values
```js
const material = new THREE.RawShaderMaterial({
    vertexShader: testVertexShader,
    fragmentShader: testFragmentShader,
    uniforms: {
        uFrequency: {value: new THREE.Vector2(10, 5)},
    }
})
```

We could now change both the z values based on x and y 
```glsl
uniform vec2 uFrequency;
void main() {
    vec4 modelPosition = modelMatrix * vec4(position, 1.0);
    // Separate it into x and y
    modelPosition.z += sin(modelPosition.x * uFrequency.x) * 0.1;
    modelPosition.z += sin(modelPosition.y * uFrequency.y) * 0.1;

    vec4 viewPosition = viewMatrix * modelPosition;
    vec4 projectedPosition = projectionMatrix * viewPosition;

    gl_Position = projectedPosition;
    vRandom = aRandom;
}
```

We could pass the elapsed time to animate our shader
```js
const material = new THREE.RawShaderMaterial({
    vertexShader: testVertexShader,
    fragmentShader: testFragmentShader,
    uniforms: {
        uFrequency: {value: new THREE.Vector2(10, 5)},
        uTime: {value: 0}
    }
})
```

Inside our tick function, we will reassign it per frame using elapsed time
```js
const tick = () =>
{
    const elapsedTime = clock.getElapsedTime()
    material.uniforms.uTime.value =  elapsedTime

    // Update controls
    controls.update()

    // Render
    renderer.render(scene, camera)

    // Call tick again on the next frame
    window.requestAnimationFrame(tick)
}
```

Then we pass it inside the [[Vertex Shader GLSL]] to animate it
```js
uniform float uTime;
void main() {
    vec4 modelPosition = modelMatrix * vec4(position, 1.0);
    // Pass inside the trigonmetric function
    modelPosition.z += sin(modelPosition.x * uFrequency.x - uTime) * 0.1;
    modelPosition.z += sin(modelPosition.y * uFrequency.y - uTime) * 0.1;

    vec4 viewPosition = viewMatrix * modelPosition;
    vec4 projectedPosition = projectionMatrix * viewPosition;

    gl_Position = projectedPosition;
    vRandom = aRandom;
}
```

![[chrome-capture-2022-8-1.gif]]

We could lessen the height by scalign the [[Three.js Mesh|mesh]]
```js
const mesh = new THREE.Mesh(geometry, material)
mesh.scale.y *= 0.5
scene.add(mesh)
```

```ad-info
collapse: open
Remember that scaling and other transformation not invloved in animation can be done by modifying the mesh

```

---
We could go one step lower by creating random spikes. In the main js file, modify the [[Three.js Geometry|geometry]] to have another attrobute filled with random values for each vertices
```js
const geometry = new THREE.PlaneGeometry(1, 1, 32, 32)

const count = geometry.attributes.position.count // length of array divide 3 cause its vector 3
const randoms = new Float32Array(count)
```

Randomized
```js
for (let i = 0; i < count; i++) {
    randoms[i] = Math.random()
}

geometry.setAttribute(
    "aRandom",
    new THREE.BufferAttribute(randoms, 1)
)
```

We could now pass it to the [[Vertex Shader]]
```glsl
uniform mat4 projectionMatrix;
uniform mat4 viewMatrix;
uniform mat4 modelMatrix;

attribute vec3 position;

// Import aRandom
attribute float aRandom;

void main() {
    vec4 modelPosition = modelMatrix * vec4(position, 1.0);
    vec4 viewPosition = viewMatrix * modelPosition;
    vec4 projectedPosition = projectionMatrix * viewPosition;
    gl_Position = projectedPosition;
}
```

Modify the z position using this value
```js
void main() {
    vec4 modelPosition = modelMatrix * vec4(position, 1.0);
    modelPosition.z += aRandom * 0.1;
    vec4 viewPosition = viewMatrix * modelPosition;
    vec4 projectedPosition = projectionMatrix * viewPosition;
    gl_Position = projectedPosition;
}
```

![[Pasted image 20220831170634.png]]

Mentions: [[Homogenous Coordinates]]

