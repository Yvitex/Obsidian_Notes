---
aliases: [InstancedMesh(), mergeBufferGeometry(), Matrix4()]
---
# Three.js Performance Tips
How can we improve our three.js performance?

#### Measurement Tools
The first thing you might want to do is to create a way to measure performance like using [[Stats.js]], keep in mind that the minimum we must sustain is 60fps.

Next step is to measure the Draw Calls using [[Spector.js]]

We could also access the [[WebGL Renderer|renderer]] information using
```js
console.log(renderer.info)
```
![[Pasted image 20220914032540.png]]

In here, we could see how many triangles or vertices we have on the scene and we could see that we have a lot, we might want to reduce it as low as possible. 

#### JS Code
The third tip might be to have a efficient and good [[Javascript]] code specially in the [[Three.js Animations]] tick function. we must avoid loops that has so many items inside. 

#### Dispose things
We cannot delete [[Three.js Mesh|mesh]] but we could delete [[Three.js Geometry|geometry]], [[Three.js Materials|material]]s etc. We could do this 
by simply using the `remove` and `dispose` method. 
```js
scene.remove(cube)
cube.geometry.dispose()
cube.material.dispose()
```

#### Avoid removing and adding lighs
Stay away from [[Three.js Light]] as possible cause they are inefficient. But if you really need to, avoid removing them cause it will create a recompilation
#### Avoid shadows
Avoid using [[Three,js Shadow]] as they are bad for performances But if you really need to, keep in mind the following:
##### Use cast and receive shadow wisely
If your [[Three.js Mesh|mesh]] don't need to cast shadow then don't, if there is no shadow that must step on the mesh then don't receive shadow. 

##### Optimize Shadow Maps
Shadow maps should be shortened using `far` and `set` method. 
##### Diable Autoupdate
This is good if your [[Three.js Mesh|mesh]] is not moving. This will cause the shadow to stop moving too
```js
renderer.shadowMap.autoUpdate = false
renderer.shadowMap.needsUpdate = true
```





#### Correct texture format
Always make your [[Three.js Textures]] value in the power of 2 because of [[Mipmapping]]. Choose either a png file or a jpg file. Compress it to reduce the weight of that texture using some compression website like [TinyPNG](https://tinypng.com/)


#### Use buffer geometry
Yeah use Buffer [[Three.js Geometry|geometry]]. Use creap geometrues like [[Basic Material]], [[Phong Material]] and [[Lambert Material]], avoid heavy material like [[Standard Material]] and [[Physical Material]]
#### Make Efficient loop codes
If you are making a loop like this
```js
for(let i = 0; i < 50; i++)
{
    const geometry = new THREE.BoxGeometry(0.5, 0.5, 0.5)
    const material = new THREE.MeshNormalMaterial()
    const mesh = new THREE.Mesh(geometry, material)
    mesh.position.x = (Math.random() - 0.5) * 10
    mesh.position.y = (Math.random() - 0.5) * 10
    mesh.position.z = (Math.random() - 0.5) * 10
    mesh.rotation.x = (Math.random() - 0.5) * Math.PI * 2
    mesh.rotation.y = (Math.random() - 0.5) * Math.PI * 2
    scene.add(mesh)
}
```

To achieve the same result but more efficient, just create a [[Three.js Mesh|mesh]] inside the loop using the same [[Three.js Geometry|geometry]] and [[Three.js Materials|material]]
```js
const geometry = new THREE.BoxGeometry(0.5, 0.5, 0.5)
const material = new THREE.MeshNormalMaterial()

for(let i = 0; i < 50; i++)
{
    const mesh = new THREE.Mesh(geometry, material)
    mesh.position.x = (Math.random() - 0.5) * 10
    mesh.position.y = (Math.random() - 0.5) * 10
    mesh.position.z = (Math.random() - 0.5) * 10
    mesh.rotation.x = (Math.random() - 0.5) * Math.PI * 2
    mesh.rotation.y = (Math.random() - 0.5) * Math.PI * 2
    scene.add(mesh)
}
```

This will have a lot of draw calls as seen in [[Spector.js]] . 
![[Pasted image 20220914135800.png]]

There is above 200 commands which is bad, we need to reduce 
To reduce the amount of draw calls, we could use the `mergeBufferGeometry()` to make this random calls into one render call
```js
import {mergeBufferGeometries} from 'three/examples/jsm/utils/BufferGeometryUtils'
```

What we could do now that we imported that method from the utilities is that we create an array of geometries which will be merged and used as a geometry to the [[Three.js Mesh|mesh]]

```js
const geometries = []
for(let i = 0; i < 50; i++)
{
    const geometry = new THREE.BoxGeometry(0.5, 0.5, 0.5)
    geometry.rotateX((Math.random() - 0.5) * Math.PI * 2)
    geometry.rotateY((Math.random() - 0.5) * Math.PI * 2)
    geometry.translate(
        (Math.random() - 0.5) * 10,
        (Math.random() - 0.5) * 10,
        (Math.random() - 0.5) * 10
    )

    geometries.push(geometry)
}
const mergedGeometry = mergeBufferGeometries(geometries)
const material = new THREE.MeshNormalMaterial()
const mesh = new THREE.Mesh(mergedGeometry, material)

scene.add(mesh)
```

[[Three.js Geometry|geometry]] will be the one to be modified by its position. 
![[Pasted image 20220914141017.png]]

The problem is, we can't move each one of the individually. The solution is using Three.js `Matrix4`.
Matrix4 requires the use of  `InstancedMesh()`, set the third parameter to 50 representing the amount of meshes we want
```js
const geometry = new THREE.BoxGeometry(0.5, 0.5, 0.5)
const material = new THREE.MeshNormalMaterial()
const mesh = new THREE.InstancedMesh(geometry, material, 50)
scene.add(mesh)
```

Create for loop, here we will create instances of the mesh using matrix4
```js
for(let i = 0; i < 50; i++)
{
    const matrix = new THREE.Matrix4() // Instantiation
    mesh.setMatrixAt(i, matrix) // Setting matrix with index value
}
```

Rotation can use [[Euler's Angle]] and position is set using [[Vector3]]. We could call the `makeRotationFromEuler()` and `setPosition()` from matrix4
```js
for(let i = 0; i < 50; i++)
{
    const position = new THREE.Vector3(
        (Math.random() - 0.5) * 10,
        (Math.random() - 0.5) * 10,
        (Math.random() - 0.5) * 10
    )

	const euler = new THREE.Euler(
        (Math.random() - 0.5) * Math.PI * 2,
        (Math.random() - 0.5) * Math.PI * 2
    )

    const matrix = new THREE.Matrix4()
    matrix.makeRotationFromEuler(euler)
    matrix.setPosition(position)
    mesh.setMatrixAt(i, matrix)
}
```

If it is need to be updated, just add this code after the mesh variable
```js
const geometry = new THREE.BoxGeometry(0.5, 0.5, 0.5)
const material = new THREE.MeshNormalMaterial()
const mesh = new THREE.InstancedMesh(geometry, material, 50)
mesh.instanceMatrix.setUsage(THREE.DynamicDrawUsage)
scene.add(mesh)
```


#### USE gzip compression
Use [[GZIP]] compression for everythin

#### Frustum Culling Technique
We could make use of frustum culling by reducing the [[Field of View]] of view in the [[Three.js Camera|camera]] and reduce its `near` and `far` 


#### Limit the pixel ration to 1 or 2
Only use a maximum pixel ratio of 2 for the [[WebGL Renderer|renderer]] 

#### Set the renderer to high-performance only if needed
We could improve the [[GPU]] performance by setting the [[WebGL Renderer|renderer]] properties like this
```js
const renderer = new THREE.WebGLRenderer({
    canvas: canvas,
    powerPreference: "high-performance"
})
```
This should only be done if needed.

#### Use antialias only if needed
No [[AntiAliasing]] is better in terms of performance rather that with anti aliasing
#### Reduce the number of post processing
Use [[Three.js Post Processing]] only if needed. Try to merge the [[Custom Passes in Three.js]] into a single pass, that is better than having multiple of them

#### When using shader, try to set the precision to lowp
When creating our own [[Shader]], we could set the precision of [[Create Shaders in Three.js|ShaderMaterial()]] and [[Create Shaders in Three.js|RawShaderMaterial()]] into "lowp"
```js
const shaderMaterial = new THREE.ShaderMaterial({
	precision: "lowp"
})
```
#### Avoid using if statement in shaders
If else statement are bad for [[Shader]] performances so avoid them as much as possible,
#### Try to not use uniforms if the value don't need to be tweaked
[[Shader Uniform]] variables are good as they could be tweaked and add into out [[Debug GUI]] but it comes with performance cost too. Use Define for variables that cannot be changed
```glsl
#define DISPLACEMENT_VALUE 1.5
```

Or import it using [[Javascript]] code but instead of using [[Shader Uniform]], use the `defines` property that will automatically import that variable to the [[GLSL]]
```js
uniforms: {
	//...
},
defines: {
	DISPLACEMENT_VALUE = 1.5
}
```

#### Do fragment calculation inside the verteex shader
[[Vertex Shader]] have less fragments than there is [[Fragments]]. So do the calculation in the [[Vertex Shader GLSL]] and transport it using the [[Shader Varying]]


# Metatags
---
###### Related: 
[[Three.js (core)]], [[Broadphase Optimization]]
Tags:
#three #javascript 