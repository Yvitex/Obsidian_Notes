---
aliases: [3d perlin noise]
---
# Raging Sea
These is through using [[Shader]]. So in the basic materials, we set it up as [[Create Shaders in Three.js|RawShaderMaterial()]]

## Initial
```js
const waterMaterial = new THREE.ShaderMaterial({
    vertexShader: waterVertex,
    fragmentShader: waterFragment,
})
```

Create a folder for shaders > water > vertex and fragment [[GLSL]]
Inside the [[Vertex Shader GLSL]] we set the first 3 main datas such as modelmatrix, viewMatrix and projectionMatrix

```glsl
void main() {
    vec4 modelPosition = modelMatrix * vec4(position, 1.0);
    vec4 cameraPosition = viewMatrix * modelPosition;
    vec4 projectionPosition = projectionMatrix * cameraPosition;
    gl_Position = projectionPosition;
}
```

To create a wave, we use the [[Trigonometric functions]] called sin in the y axis of x, we add it to the y
```glsl
void main() {
    vec4 modelPosition = modelMatrix * vec4(position, 1.0);
    // Wave
    modelPosition.y += sin(modelPosition.x);
    vec4 cameraPosition = viewMatrix * modelPosition;
    vec4 projectionPosition = projectionMatrix * cameraPosition;
    gl_Position = projectionPosition;
}
```

![[Pasted image 20220905162318.png]]

There is too much amplitude, we shall reduce it through a [[Shader Uniform]] variable so that we could modify it
```js
const waterMaterial = new THREE.ShaderMaterial({
    vertexShader: waterVertex,
    fragmentShader: waterFragment,
    
    // Uniforms
    uniforms: {
        uWaveAmplitude: {value: 0.2},
    }
})
```

we could now apply it to multiply it though the sin, not inside because the amplitude is the result of sin.
```glsl
uniform float uWaveAmplitude;

void main() {
    vec4 modelPosition = modelMatrix * vec4(position, 1.0);

	// Amplitude applied
    modelPosition.y += sin(modelPosition.x) * uWaveAmplitude;
    vec4 cameraPosition = viewMatrix * modelPosition;
    vec4 projectionPosition = projectionMatrix * cameraPosition;
    gl_Position = projectionPosition;

}
```

![[Pasted image 20220906040408.png]]

Now, we wave how high the wave is, now what we could do is to create a frequency selector. We will use a Vector2 so that is supports 2 different value
```js
const waterMaterial = new THREE.ShaderMaterial({
    vertexShader: waterVertex,
    fragmentShader: waterFragment,
    
    // Uniforms
    uniforms: {
        uWaveAmplitude: {value: 0.2}, 
        // The frequency
        uWaveFrequency: {value: new THREE.Vector2(4.0, 1.5)}
    }
})
```

Apply this value but only the x  inside the sin function
```glsl
uniform float uWaveAmplitude;
uniform vec2 uWaveAmplitude;


void main() {
    vec4 modelPosition = modelMatrix * vec4(position, 1.0);

	// Frequency Applied
    modelPosition.y += sin(modelPosition.x * uWaveAmplitude.x) * uWaveAmplitude;
    vec4 cameraPosition = viewMatrix * modelPosition;
    vec4 projectionPosition = projectionMatrix * cameraPosition;
    gl_Position = projectionPosition;
}
```


![[Pasted image 20220906041737.png]]

We also need to distort it not only using the x but also the z to increase randomness like. what we could do is to multiply it with the sin function based on z with frequency based on y
```glsl
uniform float uWaveAmplitude;
uniform vec2 uWaveAmplitude;


void main() {
    vec4 modelPosition = modelMatrix * vec4(position, 1.0);

    modelPosition.y += sin(modelPosition.x * uWaveAmplitude.x)
				    * sin(modelPosition.z * uWaveAmplityde.y) // z wave
				    * uWaveAmplitude;
    
    vec4 cameraPosition = viewMatrix * modelPosition;
    vec4 projectionPosition = projectionMatrix * cameraPosition;
    gl_Position = projectionPosition;
}
```

![[Pasted image 20220906042259.png]]



## Animation
What we could do to animate is this, apply first the uTime that will store the elapsed time which should be use to animate the object by adding it inside the sin function
```js
const waterMaterial = new THREE.ShaderMaterial({
    vertexShader: waterVertex,
    fragmentShader: waterFragment,
    
    // Uniforms
    uniforms: {
        uWaveAmplitude: {value: 0.2}, 
        uWaveFrequency: {value: new THREE.Vector2(4.0, 1.5)},
        uTime: {value: 0},
    }
})
```

We use the elapsed time to update this uTime
```js
const tick = () =>
{
    const elapsedTime = clock.getElapsedTime()
    waterMaterial.uniforms.uTime.value = elapsedTime

    // Update controls
    controls.update()
    
    // Render
    renderer.render(scene, camera)

    // Call tick again on the next frame
    window.requestAnimationFrame(tick)
}
```

Apply this to [[Vertex Shader GLSL]] by addition
```glsl
uniform float uWaveAmplitude;
uniform vec2 uWaveAmplitude;
uniform float uTime;

void main() {
    vec4 modelPosition = modelMatrix * vec4(position, 1.0);

	// Apply animation
    modelPosition.y += sin(modelPosition.x * uWaveAmplitude.x + uTime)
				    * sin(modelPosition.z * uWaveAmplityde.y + uTime) // z wave
				    * uWaveAmplitude;
    
    vec4 cameraPosition = viewMatrix * modelPosition;
    vec4 projectionPosition = projectionMatrix * cameraPosition;
    gl_Position = projectionPosition;
}
```

We could also apply a speed through  multiplication
```js
const waterMaterial = new THREE.ShaderMaterial({
    vertexShader: waterVertex,
    fragmentShader: waterFragment,
    
    // Uniforms
    uniforms: {
        uWaveAmplitude: {value: 0.2}, 
        uWaveFrequency: {value: new THREE.Vector2(4.0, 1.5)},
        uTime: {value: 0},
        uSpeed: {value: 0.7}
    }
})
```

```glsl
uniform float uWaveAmplitude;
uniform vec2 uWaveAmplitude;
uniform float uTime;
uniform float uSpeed;

void main() {
    vec4 modelPosition = modelMatrix * vec4(position, 1.0);

	// Apply animation
    modelPosition.y += sin(modelPosition.x * uWaveAmplitude.x + uTime * uSpeed)
				    * sin(modelPosition.z * uWaveAmplityde.y + uTime * uSpeed) // z wave
				    * uWaveAmplitude;
    
    vec4 cameraPosition = viewMatrix * modelPosition;
    vec4 projectionPosition = projectionMatrix * cameraPosition;
    gl_Position = projectionPosition;
}
```

![[chrome-capture-2022-8-6.gif]]


## Color
First we need to create a debugging object to change it into [[Debug GUI]]
```js
const debug = {
    depthColor: "#0000ff",
    surfaceColor: "#8888ff",
}
```

Apply this to the [[Create Shaders in Three.js|ShaderMaterial()]]
```js
const waterMaterial = new THREE.ShaderMaterial({
    vertexShader: waterVertex,
    fragmentShader: waterFragment,
    uniforms: {
        uWaveAmplitude: {value: 0.2},
        uWaveFrequency: {value: new THREE.Vector2(4.0, 1.5)},
        uTime: {value: 0},
        uSpeed: {value: 0.7},
        uDepthColor: {value: new THREE.Color(debug.depthColor)},
        uSurfaceColor: {value: new THREE.Color(debug.surfaceColor)},
    }
})
```

Apply this to the gui
```js
gui.addColor(debug, "depthColor")
    .name("uDepthColor")
    .onChange(() => {
        waterMaterial.uniforms.uDepthColor.value.set(debug.depthColor)
    })
    
gui.addColor(debug, "surfaceColor")
    .name("uSurfaceColor")
    .onChange(() => {
        waterMaterial.uniforms.uSurfaceColor.value.set(debug.surfaceColor)
    })
```

Remember that colors cannot be assigned so we must use `set` for it
Now we could test it inside the [[Fragment Shader GLSL]]
```glsl
uniform vec3 uDepthColor;
uniform vec3 uSurfaceColor;

void main(){
    gl_FragColor = vec4(uSurfaceColor, 1.0);
}
```

We could now change the color of the sea, what we could do is to mix those 2 colors depending on how the value of y

In our [[Vertex Shader GLSL]], create a varying variable that will pass the y value from position model
```glsl
uniform float uWaveAmplitude;
uniform vec2 uWaveAmplitude;
uniform float uTime;
uniform float uSpeed;
// Create a model position variable that could be pass in the next setting
varying float vModelPosition;

void main() {
    vec4 modelPosition = modelMatrix * vec4(position, 1.0);

	// get elevation value
    float elevation = sin(modelPosition.x * uWaveAmplitude.x + uTime * uSpeed)
				    * sin(modelPosition.z * uWaveAmplityde.y + uTime * uSpeed) // z wave
				    * uWaveAmplitude;

	modelPosition.y += elevation;
  
    vec4 cameraPosition = viewMatrix * modelPosition;
    vec4 projectionPosition = projectionMatrix * cameraPosition;
    gl_Position = projectionPosition;
    vModelPosition = elevation;
}
```

We could use it now to the [[Fragment Shader GLSL]]
```glsl
uniform vec3 uDepthColor;
uniform vec3 uSurfaceColor;

varying float vModelPosition;

void main(){
	vec3 mixedColor = mix(uDepthColor, uSurfaceColor, vModelPosition);
    gl_FragColor = vec4(uSurfaceColor, 1.0);
}
```

![[chrome-capture-20221-8-6.gif]]


We could correct the color intensity using the gui, add the colorMultiplier and offset values
```glsl
const waterMaterial = new THREE.ShaderMaterial({
    vertexShader: waterVertex,
    fragmentShader: waterFragment,
    uniforms: {
        uWaveAmplitude: {value: 0.2},
        uWaveFrequency: {value: new THREE.Vector2(4.0, 1.5)},
        uTime: {value: 0},
        uSpeed: {value: 0.7},
        uDepthColor: {value: new THREE.Color(debug.depthColor)},
        uSurfaceColor: {value: new THREE.Color(debug.surfaceColor)},
        // modifying values
        uColorMultiplier: {value: 0.2},
        uColorOffset: {value: 2.0}
    }
})
```

Inside the glsl, add and multiply it to the y values of ModelPosition
```glsl
uniform vec3 uDepthColor;
uniform vec3 uSurfaceColor;
uniform float uColorMultiplier;
uniform float uColorOffset;

varying float vModelPosition;

void main(){
	float colorVector = (vModelPosition + uColorOffset) * uColorMultiplier;
	vec3 mixedColor = mix(uDepthColor, uSurfaceColor, vModelPosition);
    gl_FragColor = vec4(uSurfaceColor, 1.0);
}
```

## Perlin Noise
To increase the randomness of the see and make it looks more realistic, we could add some [[Shader Pattern 29|perlin noise]]
```glsl
//	Classic Perlin 3D Noise 
//	by Stefan Gustavson
//
vec4 permute(vec4 x){return mod(((x*34.0)+1.0)*x, 289.0);}
vec4 taylorInvSqrt(vec4 r){return 1.79284291400159 - 0.85373472095314 * r;}
vec3 fade(vec3 t) {return t*t*t*(t*(t*6.0-15.0)+10.0);}

float cnoise(vec3 P){
	vec3 Pi0 = floor(P); // Integer part for indexing
	vec3 Pi1 = Pi0 + vec3(1.0); // Integer part + 1
	Pi0 = mod(Pi0, 289.0);
	Pi1 = mod(Pi1, 289.0);
	vec3 Pf0 = fract(P); // Fractional part for interpolation
	vec3 Pf1 = Pf0 - vec3(1.0); // Fractional part - 1.0
	vec4 ix = vec4(Pi0.x, Pi1.x, Pi0.x, Pi1.x);
	vec4 iy = vec4(Pi0.yy, Pi1.yy);
	vec4 iz0 = Pi0.zzzz;
	vec4 iz1 = Pi1.zzzz;

	vec4 ixy = permute(permute(ix) + iy);
	vec4 ixy0 = permute(ixy + iz0);
	vec4 ixy1 = permute(ixy + iz1);

	vec4 gx0 = ixy0 / 7.0;
	vec4 gy0 = fract(floor(gx0) / 7.0) - 0.5;
	gx0 = fract(gx0);
	vec4 gz0 = vec4(0.5) - abs(gx0) - abs(gy0);
	vec4 sz0 = step(gz0, vec4(0.0));
	gx0 -= sz0 * (step(0.0, gx0) - 0.5);
	gy0 -= sz0 * (step(0.0, gy0) - 0.5);

	vec4 gx1 = ixy1 / 7.0;
	vec4 gy1 = fract(floor(gx1) / 7.0) - 0.5;
	gx1 = fract(gx1);
	vec4 gz1 = vec4(0.5) - abs(gx1) - abs(gy1);
	vec4 sz1 = step(gz1, vec4(0.0));
	gx1 -= sz1 * (step(0.0, gx1) - 0.5);
	gy1 -= sz1 * (step(0.0, gy1) - 0.5);

	vec3 g000 = vec3(gx0.x,gy0.x,gz0.x);
	vec3 g100 = vec3(gx0.y,gy0.y,gz0.y);
	vec3 g010 = vec3(gx0.z,gy0.z,gz0.z);
	vec3 g110 = vec3(gx0.w,gy0.w,gz0.w);
	vec3 g001 = vec3(gx1.x,gy1.x,gz1.x);
	vec3 g101 = vec3(gx1.y,gy1.y,gz1.y);
	vec3 g011 = vec3(gx1.z,gy1.z,gz1.z);
	vec3 g111 = vec3(gx1.w,gy1.w,gz1.w);

	vec4 norm0 = taylorInvSqrt(vec4(dot(g000, g000), dot(g010, g010), dot(g100, g100), dot(g110, g110)));
	g000 *= norm0.x;
	g010 *= norm0.y;
	g100 *= norm0.z;
	g110 *= norm0.w;
	vec4 norm1 = taylorInvSqrt(vec4(dot(g001, g001), dot(g011, g011), dot(g101, g101), dot(g111, g111)));
	g001 *= norm1.x;
	g011 *= norm1.y;
	g101 *= norm1.z;
	g111 *= norm1.w;

	float n000 = dot(g000, Pf0);
	float n100 = dot(g100, vec3(Pf1.x, Pf0.yz));
	float n010 = dot(g010, vec3(Pf0.x, Pf1.y, Pf0.z));
	float n110 = dot(g110, vec3(Pf1.xy, Pf0.z));
	float n001 = dot(g001, vec3(Pf0.xy, Pf1.z));
	float n101 = dot(g101, vec3(Pf1.x, Pf0.y, Pf1.z));
	float n011 = dot(g011, vec3(Pf0.x, Pf1.yz));
	float n111 = dot(g111, Pf1);

	vec3 fade_xyz = fade(Pf0);
	vec4 n_z = mix(vec4(n000, n100, n010, n110), vec4(n001, n101, n011, n111), fade_xyz.z);
	vec2 n_yz = mix(n_z.xy, n_z.zw, fade_xyz.y);
	float n_xyz = mix(n_yz.x, n_yz.y, fade_xyz.x); 
	return 2.2 * n_xyz;
}
```

We could use it inside the [[Vertex Shader GLSL]], add it into the elevation of y modelPosition.
```glsl
varying float vModelPosition;
void main() {
    vec4 modelPosition = modelMatrix * vec4(position, 1.0);
    float elevation = sin(modelPosition.x * uWaveFrequency.x + uTime * uSpeed)
                    * sin(modelPosition.z * uWaveFrequency.y + uTime * uSpeed)
                    * uWaveAmplitude;
                    
    // Perlin Noise
    elevation += cnoise(vec3(modelPosition.xz, 0.2));

    modelPosition.y += elevation;
    vec4 cameraPosition = viewMatrix * modelPosition;
    vec4 projectionPosition = projectionMatrix * cameraPosition;
    
    gl_Position = projectionPosition;
    vModelPosition = elevation;
}
```

![[Pasted image 20220906142338.png]]


We could multiply the inside argument by something to increase the frequency
```glsl
varying float vModelPosition;
void main() {
    vec4 modelPosition = modelMatrix * vec4(position, 1.0);
    float elevation = sin(modelPosition.x * uWaveFrequency.x + uTime * uSpeed)
                    * sin(modelPosition.z * uWaveFrequency.y + uTime * uSpeed)
                    * uWaveAmplitude;
                    
    // Perlin Noise
    elevation += cnoise(vec3(modelPosition.xz * 10.0, 0.2));

    modelPosition.y += elevation;
    vec4 cameraPosition = viewMatrix * modelPosition;
    vec4 projectionPosition = projectionMatrix * cameraPosition;
    
    gl_Position = projectionPosition;
    vModelPosition = elevation;
}
```

![[chrome-capture-2022-8-6 (1).gif]]

It looks soo Static, we could animate it by applyign the time as the third argument
```glsl
varying float vModelPosition;
void main() {
    vec4 modelPosition = modelMatrix * vec4(position, 1.0);
    float elevation = sin(modelPosition.x * uWaveFrequency.x + uTime * uSpeed)
                    * sin(modelPosition.z * uWaveFrequency.y + uTime * uSpeed)
                    * uWaveAmplitude;
                    
    // uTime is wabed by multiplying to 0.15
    elevation += cnoise(vec3(modelPosition.xz * 10.0, uTime * 0.15));

    modelPosition.y += elevation;
    vec4 cameraPosition = viewMatrix * modelPosition;
    vec4 projectionPosition = projectionMatrix * cameraPosition;
    
    gl_Position = projectionPosition;
    vModelPosition = elevation;
}
```

Lower the frequency ok and then lessen the amplitude by dividing the overall value
```glsl
varying float vModelPosition;
void main() {
    vec4 modelPosition = modelMatrix * vec4(position, 1.0);
    float elevation = sin(modelPosition.x * uWaveFrequency.x + uTime * uSpeed)
                    * sin(modelPosition.z * uWaveFrequency.y + uTime * uSpeed)
                    * uWaveAmplitude;
                    
    // Complete config
    elevation += cnoise(vec3(modelPosition.xz * 3.0, uTime * 0.2)) * 0.15;

    modelPosition.y += elevation;
    vec4 cameraPosition = viewMatrix * modelPosition;
    vec4 projectionPosition = projectionMatrix * cameraPosition;
    
    gl_Position = projectionPosition;
    vModelPosition = elevation;
}
```

What we may want to do is to make it look sharper, to do that we apply an absolute value to the cnoise perlin noise
```glsl
varying float vModelPosition;
void main() {
    vec4 modelPosition = modelMatrix * vec4(position, 1.0);
    float elevation = sin(modelPosition.x * uWaveFrequency.x + uTime * uSpeed)
                    * sin(modelPosition.z * uWaveFrequency.y + uTime * uSpeed)
                    * uWaveAmplitude;
                    
    // Complete config
    elevation += abs(cnoise(vec3(modelPosition.xz * 3.0, uTime * 0.2)) * 0.15);

    modelPosition.y += elevation;
    vec4 cameraPosition = viewMatrix * modelPosition;
    vec4 projectionPosition = projectionMatrix * cameraPosition;
    
    gl_Position = projectionPosition;
    vModelPosition = elevation;
}
```
![[Pasted image 20220906145617.png]]

It looks blob which is the opposite of what we want, substract it instead to the elevation
```glsl
varying float vModelPosition;
void main() {
    vec4 modelPosition = modelMatrix * vec4(position, 1.0);
    float elevation = sin(modelPosition.x * uWaveFrequency.x + uTime * uSpeed)
                    * sin(modelPosition.z * uWaveFrequency.y + uTime * uSpeed)
                    * uWaveAmplitude;
                    
    // Complete config
    elevation -= abs(cnoise(vec3(modelPosition.xz * 3.0, uTime * 0.2)) * 0.15);

    modelPosition.y += elevation;
    vec4 cameraPosition = viewMatrix * modelPosition;
    vec4 projectionPosition = projectionMatrix * cameraPosition;
    
    gl_Position = projectionPosition;
    vModelPosition = elevation;
}
```

![[Pasted image 20220906145802.png]]

What just happened is that we do this
![[Pasted image 20220906145847.png]]

We turn the negatives into positives then subtract it to the elevation. 
![[Pasted image 20220906150322.png]]

Now what we could do is to increae further the randomness by overlaying the [[Shader Pattern 29|perlin noise]]. 
![[Pasted image 20220906150443.png]]

To do that, we use the thing called for loops and put there our perlin noise method call
```glsl
for (float i = 1.0; i <= 3.0; i++) {
	elevation -= abs(cnoise(vec3(modelPosition.xz * 3.0, uTime * 0.2)) * 0.15);
}
```

![[Pasted image 20220906150650.png]]

This create some weird result, wh? because we just created a perlin noise with similar height and frequency. The image diagram above shows that we need more frequency at higher iterations with lower amplitude

We could use the index to increase the frequency and decrease the amplitude
```glsl
for (float i = 1.0; i <= 3.0; i++) {
	elevation -= abs(cnoise(vec3(modelPosition.xz * 3.0 * i, uTime * 0.2)) * 0.15 * i);
}
```

![[chrome-capture-2022-8-6 (3).gif]]

Nice.
