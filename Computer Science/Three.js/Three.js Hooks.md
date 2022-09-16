---
aliases: [onBeforeCompile]
---
# Three.js Hooks
![[Pasted image 20220910014253.png]]
Is used for customized programming. We could modify and animate a model loaded with [[GLTFLoader()]] by injecting some code to its [[Shader]]

To enable hooks, we have a special material attribute called `onBeforeCompile`
```js
const material = new THREE.MeshStandardMaterial( {
	map: mapTexture,
	normalMap: normalTexture
})

material.onBeforeCompile = () => {
	console.log("Hello World")
}
```

Remember that this is a property not a method. We could call a variable inside this function which will output all access that we could do using the hooks
```js
material.onBeforeCompile = (hook) => {
	console.log(hook)
}
```

![[Pasted image 20220910012953.png]]

We could see a [[Vertex Shader]] from it, it is written with a string. Because we are using a loaded model, we are using a piece of mesh [[Physical Material]]. We could find the string of the `vertexShader` 
![[Pasted image 20220910013411.png]]

In the node module > three > src > renderers > shaders > ShaderLib > meshphysical.glsl.js
![[Pasted image 20220910013538.png]]

Include means, go and fetch those chunk of codes with the file name __ here. 
![[Pasted image 20220910014007.png]]

We have `begin_vertex` chunk and we could find its file at   node module > three > src > renderers > shaders > ShaderChunk > begin_vertex.glsl.js 
![[Pasted image 20220910014158.png]]

we could use this code to animate the loaded model. Variable `transformed` count be used to transform the model's position into different places. We could do this by replacing the `begin_vertex` with additional codes
```js
material.onBeforeCompile = (hook) => {
	hook.vertexShader = hook.vertexShader.replace(
		'#include <begin_vertex>',
		`
			#include <begin_vertex>
			transformed.y += 1.0;
		`
		)
}
```
![[Pasted image 20220910014936.png]]

As we could see, it moves and causes the [[Three,js Shadow]] to become misplaced.
What we want is to have a 3d rotation to the mesh,  So firstly, inject this code function
```glsl
mat2 get2dRotateMatrix(float _angle) {
	return mat2(cos(_angle), - sin(_angle), sin(_angle), cos(_angle));
}
```

What we want is that it should be available anywhere in the code, therefore we apply this as a global variable, to do that, we insert it after the `#include <common>`
```js
hook.vertexShader = hook.vertexShader.replace(
	    '#include <common>',
	`
	    #include <common>
	    mat2 get2dRotateMatrix(float _angle) {
	        return mat2(cos(_angle), - sin(_angle), sin(_angle), cos(_angle));
	    }
	`
)
```

We want to use this method to the transformed variable and we could access it inside the main. Defien an angle of 0.3 then apply the method as a matrix, matrix is them multiplied like we used to do it to the original transformed position
```js
hook.vertexShader = hook.vertexShader.replace(
	'#include <begin_vertex>',
	`
		#include <begin_vertex>
		float angle = 0.3;
		mat2 rotateMatrix = get2dRotateMatrix(0.3);
	`
	)
```

We could apply matrices by multiplying it
```js
hook.vertexShader = hook.vertexShader.replace(
	'#include <begin_vertex>',
	`
		#include <begin_vertex>
		float angle = 0.3;
		mat2 rotateMatrix = get2dRotateMatrix(0.3);
		transformed.xz = transfromed.xz * rotateMatrix;
	`
)
```

We only apply it in x and z cause we don't want it to rotate to y, It seems to be rotate which misplaced the shadow.
![[Pasted image 20220910023249.png]]


We could use the y position so that it will rotate base on the vertex position
```js
hook.vertexShader = hook.vertexShader.replace('#include <begin_vertex>',
`
	#include <begin_vertex>
	float angle = 0.3 * position.y;
	mat2 rotateMatrix = get2dRotateMatrix(angle);
	transformed.xz = rotateMatrix * transformed.xz;
`
)
```

![[Pasted image 20220910023538.png]]


We could rotate it by creting the uTime
```js
material.onBeforeCompile = (hook) => {
	// Create uTime
    hook.uniforms.uTime = {value: 0}
    
    hook.vertexShader = hook.vertexShader.replace(
        '#include <common>',
    `
        #include <common>

        uniform float uTime;

        mat2 get2dRotateMatrix(float _angle) {
            return mat2(cos(_angle), - sin(_angle), sin(_angle), cos(_angle));
        }
    `
    )
    // Apply the time
    hook.vertexShader = hook.vertexShader.replace('#include <begin_vertex>',
    `
        #include <begin_vertex>
        float angle = 0.3 * (position.y + uTime); 
        mat2 rotateMatrix = get2dRotateMatrix(angle);
        transformed.xz = rotateMatrix * transformed.xz;
    `
    )
}
```

We cannot access it however outside, we need to create another object that will do this
```js
const shaderValue = {
    uTime: {value: 0},
}
material.onBeforeCompile = (hook) => {
	// Create uTime
    hook.uniforms.uTime = shaderValue.uTime
   //...
    
}
```

Next is to update that time variable using the elapsed Time
```js
const tick = () =>
{
    const elapsedTime = clock.getElapsedTime()
    shaderValue.uTime.value = elapsedTime;
	// ...
}
```

Now that we are animating the  [[Three.js Imported Models]], we could then solve  a bunch of problems including [[Shadow Hooks]]

