---
aliases: [mesh]
---

# What is a Mesh?
Mesh, in terms of Three.js is a combination of [[Three.js Geometry|geometry]] and [[Three.js Materials|materials]]


## How to create a Mesh?
To create a mesh, we just need to create a new object from the Mesh class with the parameters including the [[Three.js Geometry|geometry]] and then the materials

`const mesh = new THREE.Mesh(geometry, material)`

We shall add this mesh object to the [[Three.js Scene|scene]]

`scene.add(mesh)`



#three