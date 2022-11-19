---
aliases: [renderer.setClearColor]
---
# Add More Details in Baked Material
## Background
Create a [[Debug GUI]] that will modify the background.
```js
const debug = {}
const gui = new dat.GUI({
    width: 400
})

//...

debug.clearColor = "#ff0000"
renderer.setClearColor(debug.clearColor)
gui.addColor(debug, "clearColor")
    .name("Clear Color")
    .onChange(() => {
        renderer.setClearColor(debug.clearColor)
})
```

### Fireflies
Create then the fireflies, we will use the [[Three.js Random Particles]] code to create this
```js
const fireflyGeometry = new THREE.BufferGeometry()
const fireflyCount = 30
const fireflyArray = new Float32Array(fireflyCount * 3)

for(let i = 0; i < fireflyCount; i++){
	// Assign random value via x y z
	fireflyArray[i * 3 + 0] = Math.random() * 4
	fireflyArray[i * 3 + 1] = Math.random() * 4
	fireflyArray[i * 3 + 2] = Math.random() * 4
}

// Set the array to the geometry then add materials to create mesh
fireflyGeometry.setAttribute('position', new BufferAttribute(fireflyArray, 3))
const fireflyMaterial = new THREE.PointsMaterial({size: 0.1, sizeAttenuation: true})
const firefly = new THREE.Points(fireflyGeometry, fireflyMaterial)
scene.add(firefly)
```

![[Pasted image 20220923061652.png]]

Now, the problem is how can we center the particles and position it in a reasonable manner. Just modify the position inside the loop
```js
for(let i = 0; i < fireflyCount; i++){
	// Assign random value via x y z
	fireflyArray[i * 3 + 0] = (Math.random() - 0.5) * 4
	fireflyArray[i * 3 + 1] = Math.random() * 1.5
	fireflyArray[i * 3 + 2] = (Math.random() - 0.5) * 4
}
```

![[Pasted image 20220923061905.png]]


What we could do is to replace the current material wiht [[Create Shaders in Three.js|ShaderMaterial()]]. Create a [[Vertex Shader GLSL]] and [[Fragment Shader GLSL]] with boiler plate, don't forget the `PointSize`
```glsl
void main(){
    vec4 modelPosition = modelMatrix * vec4(position, 1.0);
    vec4 viewPosition = viewMatrix * modelPosition;
    vec4 projectedPosition =  projectionMatrix * viewPosition ;
    gl_Position = projectedPosition;
    gl_PointSize = 10.0;
}
```

```glsl
void main(){
    gl_FragColor = vec4(1.0, 0.0, 0.0, 1.0);
}
```

Apply it inside the main js file
```js
import fireflyVertex from './shaders/firefly/vertex.glsl'
import fireflyFragment from './shaders/firefly/fragment.glsl'

//...

const fireflyMaterial = new THREE.ShaderMaterial({
    vertexShader: fireflyVertex,
    fragmentShader: fireflyFragment,
})

const firefly = new THREE.Points(fireflyGeometry, fireflyMaterial)
scene.add(firefly)
```

This is just like what we have done in [[Galaxy Shader]]. Like before we need to correct the point size as they are different from screen to screen in different pixel ratio, Transfer this using [[Shader Uniform]]
```js
const fireflyMaterial = new THREE.ShaderMaterial({
    vertexShader: fireflyVertex,
    fragmentShader: fireflyFragment,
    uniforms: {
        uPixelRatio: {value: Math.min(window.devicePixelRatio, 2)}
    }
})
```

Also, we need to modify this when we resize the screen
```js
window.addEventListener('resize', () => {
	fireflyMaterial.uniforms.uPixelRatio.value = Math.min(window.devicePixelRatio, 2)
}
```

We want to also control the size of the points in the gui so do this
```js
const fireflyMaterial = new THREE.ShaderMaterial({
    vertexShader: fireflyVertex,
    fragmentShader: fireflyFragment,
    uniforms: {
        uPixelRatio: {value: Math.min(window.devicePixelRatio, 2)},
        uPointScale: {value: 10.0}
    }
})

gui.add(fireflyMaterial.uniforms.uPointScale, "value").name("Point Scale").min(1.0).max(30.0).step(0.001)
```

![[Pasted image 20220923112429.png]]

In any perspective, the fireflies do not look like fireflies at all but rather just a square floating. The solution is [[Fragment Shader GLSL]]. We know the drill and it's mathematics 😂🤣😭😭😭

Use the distance and the builtin variable called `gl_PointCoord` that stores the vec2 coordinate of each points shader
```glsl
void main(){
    float distanceToCenter = distance(gl_PointCoord, vec2(0.5));
    gl_FragColor = vec4(1.0, 0.0, 0.0, distanceToCenter);
}
```

This should work if you set the [[Create Shaders in Three.js|ShaderMaterial()]]'s transparency into true. 
![[Pasted image 20220923113134.png]]

Still this is not what we want, we have a solution for that, and that is by dividing the current variable `distanceToCenter` with the dividend of a small float value

![[Pasted image 20220923113432.png]]

Just like so, notice that the graph, from high value immediately became low but it doesn't pass through zero. 

```glsl
void main(){
    float distanceToCenter = distance(gl_PointCoord, vec2(0.5));
    float strength = 0.05 / distanceToCenter;
    gl_FragColor = vec4(1.0, 1.0, 1.0, strength);
}
```

![[Pasted image 20220923113554.png]]

Still, we could see the transparent corner of the box. what we could do is to substract it with the dividend value or lower

```glsl
void main(){
    float distanceToCenter = distance(gl_PointCoord, vec2(0.5));
    float strength = 0.05 / distanceToCenter;
    gl_FragColor = vec4(1.0, 1.0, 1.0, strength);
}
```

![[Pasted image 20220923113841.png]]

We could make this better by increasing their randomness... Create a new arraw and a new attribute for the [[Fragment Shader GLSL]]
```js
const randomScaleFirefly = new Float32Array(fireflyCount)
for(let i = 0; i < fireflyCount; i++) {
    fireflyArray[i * 3 + 0] = (Math.random() - 0.5) * 4
    fireflyArray[i * 3 + 1] = Math.random() * 1.2 + 0.1
    fireflyArray[i * 3 + 2] = (Math.random() - 0.5) * 4
    
    randomScaleFirefly[i] = Math.random()
}

fireflyGeometry.setAttribute('aScale', new THREE.BufferAttribute(randomScaleFirefly, 1))
```

Import this information inside the [[Vertex Shader GLSL]]
```glsl
attribute float aScale;

void main(){
    vec4 modelPosition = modelMatrix * vec4(position, 1.0);
    vec4 viewPosition = viewMatrix * modelPosition;
    vec4 projectedPosition =  projectionMatrix * viewPosition ;
    
    gl_Position = projectedPosition;
    gl_PointSize = uPointScale * uPixelRatio * aScale;
}
```

![[Pasted image 20220923120420.png]]

Before we forgot, we also must apply the `sizeAttenuation` so that the particles are small when afar and big when close to the camera. Add this code to the [[Vertex Shader GLSL]]
```glsl
gl_PointSize *= (1.0 / - viewPosition.z);
```

Sometimes, their is a bug where the front particle will erase particles below it which is irrational. What we could do is to set the [[Three.js Particle Texturing|depthWrite()]] to false

```js
const fireflyMaterial = new THREE.ShaderMaterial({
    vertexShader: fireflyVertex,
    fragmentShader: fireflyFragment,
    transparent: true,
    uniforms: {
        uPixelRatio: {value: Math.min(window.devicePixelRatio, 2)},
        uPointScale: {value: 100.0}
    },
    depthWrite: false,
})
```

Now, we move on to the animation, set the uTime as a [[Shader Uniform]]. Update it to the tick, send it to the [[Vertex Shader GLSL]]
```js
const fireflyMaterial = new THREE.ShaderMaterial({
    vertexShader: fireflyVertex,
    fragmentShader: fireflyFragment,
    transparent: true,
    uniforms: {
	    uTime: {value: null},
        uPixelRatio: {value: Math.min(window.devicePixelRatio, 2)},
        uPointScale: {value: 100.0}
    },
    depthWrite: false,
})
```

```glsl
uniform float uTime;

void main(){
    vec4 modelPosition = modelMatrix * vec4(position, 1.0);
    
    // Animation
    modelPosition += sin(uTime)
    
    vec4 viewPosition = viewMatrix * modelPosition;
    vec4 projectedPosition =  projectionMatrix * viewPosition ;
    
    gl_Position = projectedPosition;
    gl_PointSize = uPointScale * uPixelRatio * aScale;
}
```

At this rate, there was no randomness to this movement, we could use the modelPosition x to add some difference, though it might look like a rag waving, we could increase this randomness more by multiplying to a high number.

This is the  result for sin(X) * 100  

![[Pasted image 20220926035341.png]]

```glsl
uniform float uTime;

void main(){
    vec4 modelPosition = modelMatrix * vec4(position, 1.0);
    
    // Animation
    modelPosition.y += sin(uTime + modelPosition.x * 100.0 ) * 0.2 * aScale;
    
    vec4 viewPosition = viewMatrix * modelPosition;
    vec4 projectedPosition =  projectionMatrix * viewPosition ;
    
    gl_Position = projectedPosition;
    gl_PointSize = uPointScale * uPixelRatio * aScale;
}
```

We also modify the range of movement depending on their scale and lessn it more by multiplying to 0.2.

## Portal Shader

Change the portal material to [[Create Shaders in Three.js|ShaderMaterial()]]
```js
const portalLightMaterial = new THREE.ShaderMaterial({
    vertexShader: portalVertex,
    fragmentShader: portalFragment
})
```

Set the boilerplate. 

![[Pasted image 20220926040739.png]]

Set the colors using uv to the [[Fragment Shader GLSL]] using [[Shader Varying]]

```glsl
varying vec2 vUv;
void main(){
    vec4 modelPosition = modelMatrix * vec4(position, 1.0);
    vec4 viewPosition = viewMatrix * modelPosition;
    vec4 projectedPosition = projectionMatrix * viewPosition;

    gl_Position = projectedPosition;
    vUv = uv;
}
```

```glsl
varying vec2 vUv;

void main(){
    gl_FragColor = vec4(vUv, 1.0, 1.0);
}
```

![[Pasted image 20220926042421.png]]

What we will do is to create a [[Shader Pattern 29|perlin noise]] inside it. Get the 3d classic perlin noise algorithm or copy paste this
```glsl
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

Set it to the strength variable and apply it to the rgb value of fragcolor

```glsl
void main(){
    float strength = cnoise(vec3(vUv, 0.0));
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

The result will be a bitch vblack color which we will increase in variation

![[Pasted image 20220926043949.png]]

Multiply the  vUv values with 5
```glsl
void main(){
    float strength = cnoise(vec3(vUv * 5.0, 0.0));
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

![[Pasted image 20220926044101.png]]


Send a uTime [[Shader Varying]] variable to the [[Fragment Shader GLSL]], apply it as the third argument of the 3d cnoise.

```js
const portalLightMaterial = new THREE.ShaderMaterial({
    vertexShader: portalVertex,
    fragmentShader: portalFragment,
    uniforms: {
        uTime: {value: null}
    }
})
```

Send it to [[Fragment Shader GLSL]], divide it by 2 to slow it down

```glsl
uniform float uTime;

void main(){
    float strength = cnoise(vec3(vUv * 5.0, uTime * 0.5));
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

![[chrome-capture-2022-8-26.gif]]


Else we could displace the Uv values with the cnoise like this
```glsl
void main(){
    vec2 displacedUV =  vUv + cnoise(vec3(vUv * 5.0, uTime * 0.5));
    gl_FragColor = vec4(displacedUV, 1.0, 1.0);
}
```

![[Pasted image 20220926050510.png]]

Or else, combine this 2 into 1.

```glsl
void main(){
    vec2 displacedUV =  vUv + cnoise(vec3(vUv * 5.0, uTime * 0.5));
    float strength = cnoise(vec3(displacedUV * 5.0, uTime * 0.5));
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

![[Pasted image 20220926050734.png]]


We could then add an outerglow for additional design

```glsl
void main(){
    vec2 displacedUV =  vUv + cnoise(vec3(vUv * 5.0, uTime * 0.5));
    float strength = cnoise(vec3(displacedUV * 5.0, uTime * 0.5));
	float outerGlow = distance(vUv, vec2(0.5)) * 5.0 - 1.5;
    gl_FragColor = vec4(outerGlow, outerGlow, outerGlow, 1.0);
}
```

![[Pasted image 20220926103651.png]]

Combine this effect with the previous by simple addition
```glsl
void main(){
    vec2 displacedUV =  vUv + cnoise(vec3(vUv * 5.0, uTime * 0.5));
    float strength = cnoise(vec3(displacedUV * 5.0, uTime * 0.5));
	float outerGlow = distance(vUv, vec2(0.5)) * 5.0 - 1.5;
	// Addition
	strength += outerGlow;
    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

![[Pasted image 20220926103801.png]]

It looks unfit to the scene, make it sharper using the step function
```glsl
void main(){
    vec2 displacedUV =  vUv + cnoise(vec3(vUv * 5.0, uTime * 0.1));
    float strength = cnoise(vec3(displacedUV * 5.0, uTime * 0.2));

    float outerGlow = distance(vUv, vec2(0.5)) * 5.0 - 1.5;
    strength += outerGlow;

    strength = step(-0.2, strength); // Step

    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

![[Pasted image 20220926104040.png]]

It looks extremely sharp, do not assign it to strength but rather add it to the strength and multiply it by 0.8

```glsl
void main(){
    vec2 displacedUV =  vUv + cnoise(vec3(vUv * 5.0, uTime * 0.1));
    float strength = cnoise(vec3(displacedUV * 5.0, uTime * 0.2));

    float outerGlow = distance(vUv, vec2(0.5)) * 5.0 - 1.5;
    strength += outerGlow;

    strength += step(-0.2, strength) * 0.8; // Step

    gl_FragColor = vec4(strength, strength, strength, 1.0);
}
```

![[Pasted image 20220926104158.png]]

We could start nor setting colors using [[Shader Uniform]] and with the function called [[Shader Pattern 32|mix()]].

```js
const portalLightMaterial = new THREE.ShaderMaterial({
    vertexShader: portalVertex,
    fragmentShader: portalFragment,
    uniforms: {
        uTime: {value: null},
        uStartColor: {value: new THREE.Color('#ff0000')},
        uEndColor: {value: new THREE.Color('#0000ff')},
    }
})
```

```glsl
void main(){
    vec2 displacedUV =  vUv + cnoise(vec3(vUv * 5.0, uTime * 0.1));
    float strength = cnoise(vec3(displacedUV * 5.0, uTime * 0.2));

    float outerGlow = distance(vUv, vec2(0.5)) * 5.0 - 1.5;
    strength += outerGlow;

    strength += step(-0.2, strength) * 0.8;
    vec3 finalColor = mix(uStartColor, uEndColor, strength);

    gl_FragColor = vec4(finalColor, 1.0);
}
```

Add this [[Debug GUI]]
```
debug.startColor = new THREE.Color("#ff0000")
debug.endColor = new THREE.Color("#0000ff")

// ...

gui
    .addColor(debug, 'startColor')
    .onFinishChange(() => {
        poleLightMaterial.uniforms.uStartColor.value = debug.startColor;
    })

gui
    .addColor(debug, 'endColor')
    .onFinishChange(() => {
        poleLightMaterial.uniforms.uStartColor.value = debug.startColor;
    })
```

We could then clamp the strength variable so that it won't exceed 1 or goes below 0
```js
void main(){
    vec2 displacedUV =  vUv + cnoise(vec3(vUv * 5.0, uTime * 0.1));
    float strength = cnoise(vec3(displacedUV * 5.0, uTime * 0.2));

    float outerGlow = distance(vUv, vec2(0.5)) * 5.0 - 1.5;
    strength += outerGlow;

    strength += step(-0.2, strength) * 0.8;
    strength = clamp(strength, 0.0, 1.0);
    vec3 finalColor = mix(uStartColor, uEndColor, strength);

    gl_FragColor = vec4(finalColor, 1.0);
}
```

Youve just finished a course, now practice you mf lazy ass nigga.

# Metatags
###### Related: [[3D Baking]], [[Import Baked Material to Three.js]], [[Shader]], [[Three.js Particles]], [[Debug GUI]]
###### Tags: #three 
###### Source: 

---