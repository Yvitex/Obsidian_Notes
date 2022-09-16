# Normal Material
Normal material or [[Normal Texture]] is responsible for how will the lighting, reflection, refraction etc. [[Three.js (core)]] have a class called `MeshNormalMaterial()` that is a built in way to create a normal material. 

```js
const material = new THREE.MeshNormalMaterial()
```

If applied to a geometry, it will look like this
![[Pasted image 20220816130905.png]]

This material have several property similar to [[Basic Material]] such as
- wireframe
![[Pasted image 20220816131154.png]]
- transparent
- opacity
- side

PLUS flatShading that will reveal a sqare like face of the mesh
```js
const material = new THREE.MeshNormalMaterial();
material.flatShading = true;
```

![[Pasted image 20220816131118.png]]

