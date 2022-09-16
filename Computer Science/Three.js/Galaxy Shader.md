---
aliases: [size attenuation formula, gl_PointCoord]
---
# Shader
[[Galaxy Generator]] part 2 through [[Shader]]. 

## Scaling
From the code inside the [[Galaxy Generator]], replace the [[Points Material]] by [[Create Shaders in Three.js|ShaderMaterial()]]
```js
material = new THREE.ShaderMaterial({
    size: parameters.size,
    sizeAttenuation: true,
    depthWrite: false,
    blending: THREE.AdditiveBlending,
    vertexColors: true,
})
```

This will throw an error as size and sizeAttenuation are not available with [[Shader]], delete it and replace with [[Fragment Shader]] and [[Vertex Shader]] property
```js
material = new THREE.ShaderMaterial({
    depthWrite: false,
    blending: THREE.AdditiveBlending,
    vertexColors: true,
    vertexShader: galaxyVertexShader,
    fragmentShader: galaxyFragmentShader,
})
```

Inside the [[Vertex Shader GLSL]], do the boiler plate
```glsl
void main() {
    vec4 modelPosition = modelMatrix * vec4(position, 1.0);
    vec4 viewPosition = viewMatrix * modelPosition;
    vec4 projectedPosition = projectionMatrix * viewPosition;

    gl_Position = projectedPosition;
}
```

Do the boilder plate for [[Fragment Shader GLSL]] and turn it white
```glsl
void main() {
	gl_FragColor = vec4(1.0, 1.0, 1.0, 1.0);
}
```

At this rate, you won't see anything, why? because the particles have no size, we could do the size using `gl_PointSize`
```glsl
void main() {
    vec4 modelPosition = modelMatrix * vec4(position, 1.0);
    vec4 viewPosition = viewMatrix * modelPosition;
    vec4 projectedPosition = projectionMatrix * viewPosition;

    gl_Position = projectedPosition;
    gl_PointSize = 2.0;
}
```

![[Pasted image 20220907145021.png]]


We could instead use as a [[Shader Uniform]] the constants
```js
material = new THREE.ShaderMaterial({
	depthWrite: false,
	// blending: THREE.AdditiveBlending,
	vertexColors: true,
	vertexShader: galaxyVertexShader,
	fragmentShader: galaxyFragmentShader,
	uniforms: {
	    uPointScale: {value: 8.0},
})
```

## Randomness
Right now, the points are all in the same shape, what we could do is to apply randomness using [[Shader Attributes]].
Create a container
```js
const scale = new Float32Array(parameters.cou
```

Inside the forloop we assign the values of the scale
```js
for(let i = 0; i < parameters.count; i++)
{
	// ... other codes
	scale[i] = Math.random();
}
```

The assign it as an attribute
```js
geometry.setAttribute('aPointScale', new THREE.BufferAttribute(scale, 1))
```

Multiply it to the [[Vertex Shader GLSL]]
```glsl
uniform float uPointScale;
attribute float aPointScale;

void main() {
    vec4 modelPosition = modelMatrix * vec4(position, 1.0);
    vec4 viewPosition = viewMatrix * modelPosition;
    vec4 projectedPosition = projectionMatrix * viewPosition;

    gl_Position = projectedPosition;
    
    // Wane it down
    gl_PointSize = uPointScale * aPointScale; // i set the uPointScale to 6.0
}
```

![[Pasted image 20220907154249.png]]

## Three Pixel Ratio
The problem of this now is that they may not look the same on other pc's. Some screen with 1 pixel ratio may look it appear 2 times larger than to those screen with 2 pixel ratio, what we could do is to multiply the uniform scale using the pixel ratio

We could simply do this
```js
material = new THREE.ShaderMaterial({
	depthWrite: false,
	// blending: THREE.AdditiveBlending,
	vertexColors: true,
	vertexShader: galaxyVertexShader,
	fragmentShader: galaxyFragmentShader,
	uniforms: {
	    uPointScale: {value: 8.0 * renderer.getPixelRatio()},
})
```








## Size Attenuation
In the [[Create Shaders in Three.js|ShaderMaterial()]] function, there is no size attenuation like [[Points Material]]. What we could do is to use the formula found in the [[Three.js (core)|three.js not core]] library inside one of the shader.
The formula is simply
$$1.0 / - camera.z$$

1 divide by negative camera z poistion, so that when we move the camera to the positive axis, the scale will shrink.
```glsl
uniform float uPointScale;
attribute float aPointScale;

void main() {
    vec4 modelPosition = modelMatrix * vec4(position, 1.0);
    vec4 viewPosition = viewMatrix * modelPosition;
    vec4 projectedPosition = projectionMatrix * viewPosition;

    gl_Position = projectedPosition;
    
    gl_PointSize = uPointScale * aPointScale; 
    // Size attenuation
    gl_PointSize = 1.0 / - viewPosition.z;
}
```


## Rounded Particles
It is time to modify the particles with the [[Fragment Shader GLSL]]
Of course we cant modify the color of the particles using its vertex, it is becaise each particle is its own vertex. We could do this in 3 different ways

### 1 Circles
What we could do is to use a built in variable called `gl_PointCOord` which stores the value of the very tiny poisition of each vertices
```glsl
void main() {
    gl_FragColor = vec4(gl_PointCoord, 1.0 , 1.0);
}
```

That is a vector 2. 
![[Pasted image 20220908052346.png]]

What we want are rounded particles not box so we must trim the border away using the [[Shader Pattern 22]]

```glsl
void main() {
    float strength = distance(gl_PointCoord, vec2(0.5));
    gl_FragColor = vec4(vec3(strength), 1.0);
}
```

![[Pasted image 20220908052704.png]]

We want to strengthen this up, meaning I only want 2 values, 0 and 1, and nothing in between, we could use the `step()` for this
```glsl
void main() {
    float strength = distance(gl_PointCoord, vec2(0.5));
    strength = step(0.5, strength);
    gl_FragColor = vec4(vec3(strength), 1.0);
}
```

![[Pasted image 20220908052903.png]]

It seems that it is showing the corners and not the circle, it is thre inverse of what we want so what we do is to substract it by one
```glsl
void main() {
    float strength = distance(gl_PointCoord, vec2(0.5));
    strength = step(0.5, strength);
    strength = 1.0 - strength;
    gl_FragColor = vec4(vec3(strength), 1.0);
}
```

![[Pasted image 20220908053021.png]]
![[Pasted image 20220908053101.png]]

### 2 Diffused Circles
We could do this the same way as we did before. Get the [[Shader Pattern 22]], Get the Point Coordinate and use the `distance` method to relocate the transparent slot. <u>Multiply it by 2</u> then inverse it
![[Pasted image 20220908060236.png]]

We multiply it by 2 so that it won't look like a square, cause the diagonal from the center is a bit different distance from the center and right line. 
```glsl
void main() {
    float strength = distance(gl_PointCoord, vec2(0.5));
    strength *= 2.0;
    strength = 1.0 - strength;
    gl_FragColor = vec4(vec3(strength), 1.0);
}
```

![[Pasted image 20220908060403.png]]

### 3 Easing
The third solution requires the using of easing such as `pow()`
We first get the distance of Point coordiante and center, inverse it then apply an easing to it so it will look like a circle with some fading. 
```glsl
void main() {
    float strength = distance(gl_PointCoord, vec2(0.5));
    strength = 1.0 - strength;
    strength = pow(strength, 2.0);
    gl_FragColor = vec4(vec3(strength), 1.0);
}
```

What happens here is that when we use a `pow()` to a number close to 1, like 0.95, it will yield a high number such as in the power of 2, it will became 0.9025 but if it is 0.3, then it will yield a much lower value such as 0.09. 
![[Pasted image 20220908061008.png]]

It is fast to decrease and increase. Set the power to 10.0
![[Pasted image 20220908061053.png]]


## Colors
We could applu colors in it, and because we already have an installed color based on [[Galaxy Generator]] atttribute. We could apply it inside the [[Vertex Shader]]
```glsl
attribute vec3 color;
```

This will produce an error, it is because we are using [[Create Shaders in Three.js|ShaderMaterial()]] and this method will automatically import the color attribute if we activate the `vertexColor` Attribute
```js
material = new THREE.ShaderMaterial({
        depthWrite: false,
        blending: THREE.AdditiveBlending,
        vertexColors: true, // vectexColor means use the attribute color
        vertexShader: galaxyVertexShader,
        fragmentShader: galaxyFragmentShader,
        uniforms: {
            uPointScale: {value: 30.0 * renderer.getPixelRatio()}, // change to 30
        }
    })
```

And also, we can't change the color inside the [[Vertex Shader]], we could do that inside [[Fragment Shader]] so we pass it as a [[Shader Varying]] attribute
```glsl
varying vec3 vColor;

void main() {
	// ...
	vColor = color;
}
```

Mix the color black and this color using the strength as the reference
```glsl
varying vec3 vColor;

void main() {
    float strength = distance(gl_PointCoord, vec2(0.5));
    strength = 1.0 - strength;
    strength = pow(strength, 10.0);

	// Mix Color
    vec3 mixedColor = mix(vec3(0.0), vColor, strength);
    gl_FragColor = vec4(vec3(mixedColor), 1.0);
}
```

![[Pasted image 20220909040419.png]]




## Animation
Animation could be done inside the [[Vertex Shader]]. In our case, what we want is to move the particles based on its distance while increasing it over time. ![[Pasted image 20220909043708.png]]

We will be animating with z and x. We will first need to get the angle between the x and z
```glsl
vec4 modelPosition = modelMatrix * vec4(position, 1.0);
float angle = atan(modelPosition.x, modelPosition.z);
```

Next is to calculate the distance of each vertices awar from the center
```glsl
vec4 modelPosition = modelMatrix * vec4(position, 1.0);
float angle = atan(modelPosition.x, modelPosition.z);
float distance = length(modelPosition.xz);
```

Next is to calculate the supposed offset or movement.
```glsl
vec4 modelPosition = modelMatrix * vec4(position, 1.0);
float angle = atan(modelPosition.x, modelPosition.z);
float distance = length(modelPosition.xz);
float angleOffset = (1.0 / distance); 
```

1 divide distance as we need the need it to be inverted, as in, we want the particles to move past near the center so if the distance is low, the speed must be high. 
Now we need the uTime from the elapsedTime, we already know how to do this, just get the elapsed time value using a [[Shader Uniform]], multiply it to the offset then lower it
```glsl
vec4 modelPosition = modelMatrix * vec4(position, 1.0);
float angle = atan(modelPosition.x, modelPosition.z);
float distance = length(modelPosition.xz);
float angleOffset = (1.0 / distance) * uTime * 0.2; 
```

Add the offset to the angle
```glsl
vec4 modelPosition = modelMatrix * vec4(position, 1.0);
float angle = atan(modelPosition.x, modelPosition.z);
float distance = length(modelPosition.xz);
float angleOffset = (1.0 / distance) * uTime * 0.2; 
angle += angleOffset;
```

Rotate the z and x using [[Trigonometric functions]]
```glsl
vec4 modelPosition = modelMatrix * vec4(position, 1.0);
float angle = atan(modelPosition.x, modelPosition.z);
float distance = length(modelPosition.xz);
float angleOffset = (1.0 / distance) * uTime * 0.2; 
angle += angleOffset;

modelPosition.x = sin(angle);
modelPosition.z = cos(angle);
```
![[chrome-capture-2022-8-9.gif]]


This happen because we forgot to re apply the distance
```glsl
vec4 modelPosition = modelMatrix * vec4(position, 1.0);
float angle = atan(modelPosition.x, modelPosition.z);
float distance = length(modelPosition.xz);
float angleOffset = (1.0 / distance) * uTime * 0.2; 
angle += angleOffset;

modelPosition.x = sin(angle) * distance;
modelPosition.z = cos(angle) * distance;
```
![[chrome-capture-2022-8-9 (1).gif]]


## Adding More Randomness
Still, overtime, this will do a vertical ribbon like effect, to prevent that, we need to apply the randomness after the spin

Create another float container called `randomness`
```js
const randomness = new Float32Array(parameters.count * 3)
```

Remove the randomness from the position attribute and separate it to be applued on the randomness attribtue
```js
for(let i = 0; i < parameters.count; i++)
    {
        const i3 = i * 3
        const radius = Math.random() * parameters.radius
        const branchAngle = (i % parameters.branches) / parameters.branches * Math.PI * 2

		// Remove randomness
        positions[i3    ] = Math.cos(branchAngle) * radius
        positions[i3 + 1] = 0
        positions[i3 + 2] = Math.sin(branchAngle) * radius

		// Separate randomness
        const randomX = Math.pow(Math.random(), parameters.randomnessPower) * (Math.random() < 0.5 ? 1 : - 1) * parameters.randomness * radius
        const randomY = Math.pow(Math.random(), parameters.randomnessPower) * (Math.random() < 0.5 ? 1 : - 1) * parameters.randomness * radius
        const randomZ = Math.pow(Math.random(), parameters.randomnessPower) * (Math.random() < 0.5 ? 1 : - 1) * parameters.randomness * radius

		// Apply Randomenss
        randomness[i3] = randomX;
        randomness[i3 + 1] = randomY;
        randomness[i3 + 2] = randomZ;

        // Color
        const mixedColor = insideColor.clone()
        mixedColor.lerp(outsideColor, radius / parameters.radius)

        colors[i3    ] = mixedColor.r
        colors[i3 + 1] = mixedColor.g
        colors[i3 + 2] = mixedColor.b

        scale[i] = Math.random() * 2;
    }
```

Now, send it as an attribute
```js
geometry.setAttribute('aRandomness', new THREE.BufferAttribute(randomness, 3))
```

After the spin, we will add the randomness to the equation of the position
```glsl
void main() {

    vec4 modelPosition = modelMatrix * vec4(position, 1.0);

    float angle = atan(modelPosition.x, modelPosition.z);
    float distanceFromCenter = length(modelPosition.xz);
    float angleOffset = (1.0 / distanceFromCenter) * uTime * 0.2;

    angle += angleOffset;
    
    modelPosition.x = sin(angle) * distanceFromCenter;
    modelPosition.z = cos(angle) * distanceFromCenter;

	// Randomness
    modelPosition.xyz += aRandomness;

    vec4 viewPosition = viewMatrix * modelPosition;
    vec4 projectedPosition = projectionMatrix * viewPosition;
    
    gl_Position = projectedPosition;
    gl_PointSize = uPointScale * aPointScale;
    gl_PointSize *= (0.1 / -viewPosition.z);

    vColor = color;
}
```