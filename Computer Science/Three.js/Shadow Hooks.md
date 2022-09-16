# Shadow Hooks
![[chrome-capture-2022-8-12.gif]]

As we could see, using [[Three.js Hooks]] causes some irrationality between the movement of shadows. Meaning that the [[Three,js Shadow]] doesn't really move in accordance with the model. 

Shadown map is produce when the [[Three.js Light]] use its [[Three.js Camera|camera]] to see what it could see then creates a shadow using it. All [[Three.js Materials|material]] in the [[Three.js Scene|scene]] are repalced by a spacific material called [[Depth Material]]. 

What we could do is t replace that depthmaterial using the `customDepthMaterial`  property into another [[Depth Material]] that we could control

Create a depth material with `depthPacking`
```js
const depthMaterial = new THREE.MeshDepthMaterial({
	depthPacking: THREE.RGBADepthPacking,
})
```

We could see this thing if we replace the [[Three.js Imported Models]]'s material
```js
gltfLoader.load(
    '/models/LeePerrySmith/LeePerrySmith.glb',
    (gltf) =>
    {
        // Model
        const mesh = gltf.scene.children[0]
        mesh.rotation.y = Math.PI * 0.5
        mesh.material = depthMaterial //depthMaterial
        scene.add(mesh)
        
        // Update materials
        updateAllMaterials()
    }
)
```

![[Pasted image 20220912022707.png]]

Insert this custome [[Depth Material]] to to right property
```js
gltfLoader.load(
    '/models/LeePerrySmith/LeePerrySmith.glb',
    (gltf) =>
    {
        // Model
        const mesh = gltf.scene.children[0]
        mesh.rotation.y = Math.PI * 0.5
        mesh.material = material
        mesh.customDepthMaterial = depthMaterial
        scene.add(mesh)
        
        // Update materials
        updateAllMaterials()
    }
)
```

![[Pasted image 20220912022858.png]]


We could now create a [[Three.js Hooks]] for that material
```js
depthMaterial.onBeforCompile = (shader) => {
	shader.vertexShader = shader.vertexShader.replace(
		'#include <begin_vertex>',
		`
			#include <begin_vertex>
		`
	)
}
```

We could check this if this would work by moving the `transformed` variable
```js
depthMaterial.onBeforCompile = (shader) => {
	shader.vertexShader = shader.vertexShader.replace(
		'#include <begin_vertex>',
		`
			#include <begin_vertex>
			transformed.y = 2.0;
		`
	)
}
```

![[Pasted image 20220912023808.png]]


What we could do is just to copy the code we used to rotate the [[Three.js Imported Models]] in the [[Three.js Hooks]]
```js
depthMaterial.onBeforeCompile = (hook) => {
    hook.uniforms.uTime = shaderValue.uTime
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
    hook.vertexShader = hook.vertexShader.replace('#include <begin_vertex>',
    `
        #include <begin_vertex>
        float angle = 0.8 * (position.y + uTime);
        mat2 rotateMatrix = get2dRotateMatrix(angle);
        transformed.xz = rotateMatrix * transformed.xz;
    `
    )
}
```

The shadows are now moving similar to our model. Now the problem  is the skin of the model which has a worng shadow value
![[Pasted image 20220912030302.png]]

This is caused by the [[Normal Texture]], even though we rotated the vertices, it does not do it in the [[Normal Texture]]. what we coul do is to modify the normals using hooks. If we look at the code inside node_modules > three > src > renderers > shaders > ShaderLib > meshPhysical.glsl.js

![[Pasted image 20220912030550.png]]

We just don't have the `begin_vertex` but we also have the `beginnormal_vertex` chunk. If we look into that chunk we see this

![[Pasted image 20220912030754.png]]

We could modify the `objectNormal` variable to twist the shadow. 
Using our [[Three.js Hooks]] for the `material` variable, the material of the [[Three.js Imported Models]], we could do this modifucation
```js
depthMaterial.onBeforeCompile = (hook) => {
    hook.uniforms.uTime = shaderValue.uTime
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
    
    hook.vertexShader = hook.vertexShader.replace('#include <begin_vertex>',
    `
        #include <begin_vertex>
        float angle = 0.8 * (position.y + uTime);
        mat2 rotateMatrix = get2dRotateMatrix(angle);
        transformed.xz = rotateMatrix * transformed.xz;
    `
    )
}
```

Add another hook to modify the normals
```js
material.onBeforeCompile = (hook) => {
    hook.uniforms.uTime = shaderValue.uTime
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

	// Normal Mods
    hook.vertexShader = hook.vertexShader.replace(
        '#include <beginnormal_vertex>',
        `
            #include <beginnormal_vertex>
            float angle = 0.8 * (position.y + uTime);
            mat2 rotateMatrix = get2dRotateMatrix(angle);
            objectNormal.xz = rotateMatrix * objectNormal.xz;
        `
    )
    hook.vertexShader = hook.vertexShader.replace('#include <begin_vertex>',
    `
        #include <begin_vertex>
        float angle = 0.8 * (position.y + uTime);
        mat2 rotateMatrix = get2dRotateMatrix(angle);
        transformed.xz = rotateMatrix * transformed.xz;
    `
    )
}
```

We just copy the code from the vertex mods so that it will be the same, though it will cause an error. Why? because we are redeclaring the `angle` and `rotateMatrix` as new variable. To fix this we could just erase the second one.

![[Pasted image 20220912031949.png]]

![[chrome-capture-2022-8-12 (1).gif]]