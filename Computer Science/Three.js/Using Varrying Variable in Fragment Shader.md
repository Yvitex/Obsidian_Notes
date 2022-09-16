# Using Varrying Variable in Fragment Shader
The code for vertex shader is like this, we just add a varying data type and assign it a certain value
```glsl
uniform mat4 projectionMatrix;
uniform mat4 viewMatrix;
uniform mat4 modelMatrix;

attribute vec3 position;
attribute float aRandom;

// Create a varying variable
varying float vRandom;

void main() {
    vec4 modelPosition = modelMatrix * vec4(position, 1.0);
    modelPosition.z += aRandom * 0.1;
    
    vec4 viewPosition = viewMatrix * modelPosition;
    vec4 projectedPosition = projectionMatrix * viewPosition;

    gl_Position = projectedPosition;

	// Assign the varying variable
    vRandom = aRandom;
}
```

Then we could pass it into the fragment shader like this
```glsl
precision mediump float;

varying float vRandom;
void main() {
    gl_FragColor = vec4(1.0, vRandom, 0.0, 1.0);
}

```

Now, our green will depend on the z position of the [[Vertex Shader GLSL]]. 
![[Pasted image 20220901044550.png]]

