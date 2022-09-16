---
aliases: [ShaderPass()]
---
# Custom Passes in Three.js
We could create our own [[Three.js Post Processing]] using `ShaderPass()`
```js
import {ShaderPass} from 'three/examples/jsm/postprocessing/ShaderPass'
```

## Custom Tint
We could apply the [[GLSL]] code as a parameter here
```js
const customShader = new ShaderPass()
composer.addPass(customShader) 
```

We could create our own object that will store the code
```js
const postProcessingShader = {
	uniforms: {},
	vertexShader: ``,
	fragmentShader: ``,
}
```

Create the basic boilder plate
```js
const postProcessingShader = {
    uniforms: {
    
    },
    vertexShader: `
        void main() {
            gl_Position = projectionMatrix * viewMatrix * vec4(position, 1.0);
        }
    `,
    fragmentShader: `
        void main() {
            gl_FragColor = vec4(1.0, 0.0, 0.0, 1.0);
        }
    `,
}
```

Then apply it to the ShaderPass()
```js
const customShader = new ShaderPass(postProcessingShader)
composer.addPass(customShader) 
```

![[Pasted image 20220913093143.png]]


In order to fetch the previous textures prior to applying the [[Three.js Post Processing|render target]], we could use the uniforms builtin `tDiffuse` variable
```ad-Attention
title: Do Not Change the name tDiffuse


```

```js
const postProcessingShader = {
    uniforms: {
	    tDiffuse: {value: null} // tDiffuse //
    },
    vertexShader: `
        void main() {
            gl_Position = projectionMatrix * viewMatrix * vec4(position, 1.0);
        }
    `,
    fragmentShader: `
        void main() {
            gl_FragColor = vec4(1.0, 0.0, 0.0, 1.0);
        }
    `,
}
```

Fetch this to the fragment shader as `sampler2D` and use it at `texture2D` method
```js
const postProcessingShader = {
    uniforms: {
	    tDiffuse: {value: null} // tDiffuse //
    },
    vertexShader: `
        void main() {
            gl_Position = projectionMatrix * viewMatrix * vec4(position, 1.0);
        }
    `,
    fragmentShader: `

		uniform sampler2D tDiffuse;

        void main() {

			vec4 color = texture2D(tDiffuse, )
            gl_FragColor = vec4(1.0, 0.0, 0.0, 1.0);
        }
    `,
}
```

texture2D needs 2 argument, the texture and the UV coordinates, we don't have these coordinates so we pass it as [[Shader Varying]]
```js
const postProcessingShader = {
    uniforms: {
	    tDiffuse: {value: null} // tDiffuse //
    },
    vertexShader: `
		varying vec2 vUv;
        void main() {
            gl_Position = projectionMatrix * viewMatrix * vec4(position, 1.0);
            vUv = uv;
        }
    `,
    fragmentShader: `

		uniform sampler2D tDiffuse;
		varying vec2 vUv;

        void main() {
			vec4 color = texture2D(tDiffuse, vUv);
            gl_FragColor = vec4(1.0, 0.0, 0.0, 1.0);
        }
    `,
}
```

Now we have the images back
![[Pasted image 20220913095232.png]]

We could create some uniform properties to it to adjust the tint, for example, inside the uniforms do this
```js
uniforms: {
	tDiffuse: {value: null},
	uTint: {value: null}
},
```

We could add this to the [[Fragment Shader]]
```js
const postProcessingShader = {

    uniforms: {
		tDiffuse: {value: null},
		uTint: {value: null}
	},
	
    vertexShader: `
		varying vec2 vUv;
        void main() {
            gl_Position = projectionMatrix * viewMatrix * vec4(position, 1.0);
            vUv = uv;
        }
    `,
    
    fragmentShader: `
		uniform vec3 uTint;
		uniform sampler2D tDiffuse;
		varying vec2 vUv;

        void main() {
			vec4 color = texture2D(tDiffuse, vUv);
			color.rgb += uTint;
            gl_FragColor = vec4(1.0, 0.0, 0.0, 1.0);
        }
    `,
}
```

We could access it using the [[Custom Passes in Three.js|ShaderPass()]] `material` property. Assign a [[Vector3]] to be modified
```js
const customShader = new ShaderPass(postProcessingShader)
customShader.material.uniforms.uTint.value = new THREE.Vector3()
```

Create a [[Debug GUI]]
```js
gui.add(customShader.material.uniforms.uTint.value, 'x').min(0).max(1).step(0.0001).name("red")
gui.add(customShader.material.uniforms.uTint.value, 'y').min(0).max(1).step(0.0001).name("blue")
gui.add(customShader.material.uniforms.uTint.value, 'z').min(0).max(1).step(0.0001).name("green")
```
![[chrome-capture-2022-8-13.gif]]


## Custom Displacement Waves
We could do this by simply changing the position of the UV values
```js
fragmentShader: `
	varying vec2 vUv;
	uniform vec3 uTint;    
	uniform sampler2D tDiffuse;

	void main() {
		vec2 modUv = vec2(
			vUv.x,
			vUv.y + sin(vUv.x * 10.0) * 0.1
		);

		vec4 color = texture2D(tDiffuse, modUv);
		gl_FragColor = color;
	}
`,
```

Just change the value of uV where y is added with sinusoidal value along with previous texture
![[Pasted image 20220913104146.png]]

We could animate it by applying uTime
```js
fragmentShader: `
	varying vec2 vUv;
	uniform vec3 uTint;    
	uniform sampler2D tDiffuse;
	uniform float uTime;

	void main() {
		vec2 modUv = vec2(
			vUv.x,
			vUv.y + sin(vUv.x * 10.0 + uTime) * 0.1
		);

		vec4 color = texture2D(tDiffuse, modUv);
		gl_FragColor = color;
	}
`,
```


## Futuristic Hex Screen
We will use this texture
![[Pasted image 20220913141818.png]]

Create a uniform that will import it
```js
uniforms: {
	tDiffuse: {value: null},
	uNormalMap: {value: null}
}
```

`uNormalMap` will adapt the loaded [[Normal Texture]] there from the [[Custom Passes in Three.js|ShaderPass()]]
```js
const displacementShader = new ShaderPass(displacementPass)
displacementShader.material.uniforms.uNormalMap.value = textureLoader.load("/textures/interfaceNormalMap.png")
composer.addPass(displacementShader)
```

Then in the [[Fragment Shader]]. we will use the uNormalMap using `texture2D`
```js
fragmentShader: `

	varying vec2 vUv;
	uniform vec3 uTint;    

	uniform sampler2D tDiffuse;
	uniform float uTime;
	uniform sampler2D uNormalMap;

	void main() {
		// Normal Map
		vec3 normalColor = texture2D(uNormalMap, vUv).xyz * 2.0 - 1.0;
		vec4 color = texture2D(tDiffuse, modUv);
		gl_FragColor = color;
	}
`,
```

Set the normal map as a displacement by adding it to the vUv
```js
fragmentShader: `

	varying vec2 vUv;
	uniform vec3 uTint;    

	uniform sampler2D tDiffuse;
	uniform float uTime;
	uniform sampler2D uNormalMap;

	void main() {
		// Normal Map
		vec3 normalColor = texture2D(uNormalMap, vUv).xyz * 2.0 - 1.0;
		vec3 modUv = vUv + normalColor.rgb * 0.1;
		vec4 color = texture2D(tDiffuse, modUv);
		gl_FragColor = color;
	}
`,
```

![[Pasted image 20220913143119.png]]

Now there is a slight distortion
What we could do is tor apply a light in the edges. The algorithm should be to create a light location which is [[Normallize]]d, calculate the [[Dot Product]] of the normalized light direction and the normalMap, apply the result to the overall color
```js
fragmentShader: `

	varying vec2 vUv;
	uniform vec3 uTint;    

	uniform sampler2D tDiffuse;
	uniform float uTime;
	uniform sampler2D uNormalMap;

	void main() {
		// Normal Map
		vec3 normalColor = texture2D(uNormalMap, vUv).xyz * 2.0 - 1.0;
		vec3 modUv = vUv + normalColor.rgb * 0.1;
		vec4 color = texture2D(tDiffuse, modUv);

		// Light Direction
        vec3 lightDirection = normalize(vec3(-1.0, 1.0, 0.0));
        float lightness = dot(normalColor, lightDirection);
        color.rgb += lightness * 2.0;
	
		gl_FragColor = color;
	}
`,
```

![[Pasted image 20220913143956.png]]

We could see some value which are too dark, [[Shader Pattern 32|clamp()]] the values so that it won't exceed below 0 or above 1
```js
fragmentShader: `

	varying vec2 vUv;
	uniform vec3 uTint;    

	uniform sampler2D tDiffuse;
	uniform float uTime;
	uniform sampler2D uNormalMap;

	void main() {
		// Normal Map
		vec3 normalColor = texture2D(uNormalMap, vUv).xyz * 2.0 - 1.0;
		vec3 modUv = vUv + normalColor.rgb * 0.1;
		vec4 color = texture2D(tDiffuse, modUv);

		// Light Direction
        vec3 lightDirection = normalize(vec3(-1.0, 1.0, 0.0));
        float lightness = clamp(dot(normalColor, lightDirection), 0.0, 1.0);
        color.rgb += lightness * 2.0;
	
		gl_FragColor = color;
	}
`,
```
![[Pasted image 20220913144213.png]]

---
Related: [[GLSL]], [[Shader]], [[Shader Varying]], [[Shader Uniform]], [[Fragment Shader]], [[Vertex Shader]], [[Normal Texture]], [[Normallize]], [[Dot Product]]. [[Three.js Post Processing]]
