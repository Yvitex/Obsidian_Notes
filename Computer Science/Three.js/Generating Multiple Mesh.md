# Multiple Mesh
We could generate [[Three.js Mesh|mesh]], a thousand of them using for loops
```js
for (let i = 0; i < 100; i++) {
  const donutGeometry =  new THREE.TorusBufferGeometry(0.3, 0.2, 20, 45);
  const donutMaterial = new THREE.MeshMatcapMaterial();
  donutMaterial.matcap = textTexture;
  const donutMesh = new THREE.Mesh(donutGeometry, donutMaterial)
  donutMesh.position.x = ( Math.random() - 0.5 ) * 12;
  donutMesh.position.y = ( Math.random() - 0.5 ) * 12;
  donutMesh.position.z = ( Math.random() - 0.5 ) * 12;
  donutMesh.rotation.x = Math.random() * Math.PI;
  donutMesh.rotation.y = Math.random() * Math.PI;

  // donutMesh.rotation.z = Math.random() * Math.PI;
  const scale = Math.random()
  donutMesh.scale.set(scale, scale, scale)
  scene.add(donutMesh);
}
```

This has random position, rotation and scaling. Position needs to be substracted to -0.5 to have also a negative value. Scake needs to have similar scale size in x, y, z axis. 

![[Pasted image 20220817150547.png]]

The problem here is that it is slow. 
If we measure the time using `console.time()`
```js
console.time("donut")
for (let i = 0; i < 100; i++) {
  const donutGeometry =  new THREE.TorusBufferGeometry(0.3, 0.2, 20, 45);
  const donutMaterial = new THREE.MeshMatcapMaterial();
  donutMaterial.matcap = textTexture;
  const donutMesh = new THREE.Mesh(donutGeometry, donutMaterial)
  donutMesh.position.x = ( Math.random() - 0.5 ) * 12;
  donutMesh.position.y = ( Math.random() - 0.5 ) * 12;
  donutMesh.position.z = ( Math.random() - 0.5 ) * 12;
  donutMesh.rotation.x = Math.random() * Math.PI;
  donutMesh.rotation.y = Math.random() * Math.PI;

  // donutMesh.rotation.z = Math.random() * Math.PI;
  const scale = Math.random()
  donutMesh.scale.set(scale, scale, scale)
  scene.add(donutMesh);
}
console.timeEnd("donut")
```

![[Pasted image 20220817150659.png]]

It took 122 millisecond. What we could do to optimize this is by making the donut [[Three.js Geometry|geometry]] and [[Three.js Materials|material]] as a global variable
```js
console.time("donut")
const donutGeometry =  new THREE.TorusBufferGeometry(0.3, 0.2, 20, 45);
const donutMaterial = new THREE.MeshMatcapMaterial();

donutMaterial.matcap = textTexture;
for (let i = 0; i < 100; i++) {

  const donutMesh = new THREE.Mesh(donutGeometry, donutMaterial)
  donutMesh.position.x = ( Math.random() - 0.5 ) * 12;
  donutMesh.position.y = ( Math.random() - 0.5 ) * 12;
  donutMesh.position.z = ( Math.random() - 0.5 ) * 12;
  donutMesh.rotation.x = Math.random() * Math.PI;
  donutMesh.rotation.y = Math.random() * Math.PI;
  const scale = Math.random()
  donutMesh.scale.set(scale, scale, scale)
  scene.add(donutMesh);
}

console.timeEnd("donut")
```

![[Pasted image 20220817150957.png]]
