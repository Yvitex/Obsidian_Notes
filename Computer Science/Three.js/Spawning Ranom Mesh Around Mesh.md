# Spawn
![[Pasted image 20220819095511.png]]

A way to spawn randomly aroung a thing without spawnign inside the thing and outside of the plane
```js
const graveGeometry = new THREE.BoxBufferGeometry(0.6, 0.8, 0.2);
const graveMaterial = new THREE.MeshStandardMaterial({color: "#b2b6b1"})

for (let i = 0; i < 50; i++){
    const angle = Math.random() * Math.PI * 2
    const x = Math.sin(angle)
    const z = Math.cos(angle)
    const radius = 3.5 + Math.random() * 6

    const graveMesh = new THREE.Mesh(graveGeometry, graveMaterial);
    graveMesh.position.x = x * radius
    graveMesh.position.z = z * radius

    graveMesh.rotation.z =(Math.random() - 0.5) * 0.4 //will rotate it randomly slightlty
    graveMesh.rotation.y =(Math.random() - 0.5) * 0.8
    graves.add(graveMesh);
}
```

