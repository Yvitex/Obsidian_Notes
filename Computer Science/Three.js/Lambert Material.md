# Lambert Material
Won't show the [[Three.js Geometry|geometry]] unless acted by a light

```js
const material = new THREE.MeshLambertMaterial();
```

![[Pasted image 20220816162425.png]]

we need to add a [[Three,js Lighting]]
We use the [[Ambient Light]] class and [[Point Light]] class. 
```js
const ambientLight = new THREE.AmbientLight("#fff", 0.5);
const pointLight = new THREE.PointLight("#fff", 0.5);

scene.add(ambientLight, pointLight)
```

![[Pasted image 20220816162557.png]]

