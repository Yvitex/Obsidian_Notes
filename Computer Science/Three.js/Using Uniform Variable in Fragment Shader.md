# Using Uniform Variable in Fragment Shader
We could pass color as a constant like this. In the [[Create Shaders in Three.js|RawShaderMaterial()]]
```js
const material = new THREE.RawShaderMaterial({
    vertexShader: testVertexShader,
    fragmentShader: testFragmentShader,
    uniforms: {
        uFrequency: {value: new THREE.Vector2(10, 5)},
        uTime: {value: 0},
        uTexture: {value: new THREE.Color("orange")}
    }
})
```

Then we could now pass it in the [[Fragment Shader GLSL]] as a vec3
```glsl
precision mediump float;
// Vector 3
uniform vec3 uTexture;
void main() {
    gl_FragColor = vec4(uTexture, 1.0);
}
```

![[Pasted image 20220901141125.png]]
