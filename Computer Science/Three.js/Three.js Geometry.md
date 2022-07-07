---
aliases: [geometry, vertices, faces]
---

# What is Three.js Geometry?
A figure or a shape we create as a [[Three.js Mesh|mesh]] property and also for [[Particles]]

## Basic Cube Geometry
Three.js already has a specified class in creating a cube called **BoxGeometry** and we will just need to create a copy of it

```js
const geometry = new THREE.BoxGeometry(1, 1, 1)
```
The parameters we use is the x, y, z size of the geometry. In actuality, we could also specify the widthSegment, heightSegment, depthSegment so there are total of 6 parameters. 
![[Pasted image 20220706113737.png]]

Segments divide the surface to create triangles. The image above is when we specify the segments as 1 which is the default value. This will happen if we set the segments into 2.
![[Pasted image 20220706113857.png]]

We have 8 faces. In code, we do this
```js
const geometry = new THREE.BoxGeometry(1, 1, 1, 2, 2, 2);
```

We do this to create more detail to a [[Three.js Mesh|mesh]] or object. We could see the amount of segments we have by setting the [[Three.js Materials|materials]] object to `wireframe: true`
```js
const material = new THREE.MeshBasicMaterial({color: "red", wireframe: true})
```
![[Pasted image 20220706114809.png]]

In blender, we have 3 parts of a 3d object. Edge, vertices and faces. In constructing geometries in [[Three.js (core)]]. It is one and the same  except that faces are defines as a connection between 3 vertices forming a triangle. 
![[Pasted image 20220706111406.png]]

The cross is the vertices, the lines are the edge and the solid shape that forms within this si called the face creating a triangular shape is called faces. 

## Vertices can store each of the following
- [[Position (Three.js)|position]]
- UV coordinates
- color
- normals
- etc...

These are specifically the case when we are creating [[Particles]]

## Built In Geometries
- Box ![[Pasted image 20220706113124.png]]
- Plane ![[Pasted image 20220706113141.png]]
- Circle ![[Pasted image 20220706113153.png]]
- Cone ![[Pasted image 20220706113205.png]]
- Cylinder ![[Pasted image 20220706113217.png]]
- Ring ![[Pasted image 20220706113230.png]]
- Torus ![[Pasted image 20220706113244.png]]
- TorusKnot ![[Pasted image 20220706113256.png]]
- Dodecahedron ![[Pasted image 20220706113307.png]]
- Octahedron ![[Pasted image 20220706113344.png]]
- Tetrahedron ![[Pasted image 20220706113354.png]] ![[Pasted image 20220706113422.png]]
- Icosehadron ![[Pasted image 20220706113439.png]]
- Sphere ![[Pasted image 20220706113452.png]]
- Shape ![[Pasted image 20220706113510.png]]
- Tube ![[Pasted image 20220706113521.png]]
- Extrude ![[Pasted image 20220706113532.png]]
- Lathe ![[Pasted image 20220706113550.png]]
- Text ![[Pasted image 20220706113602.png]]

Now, how can we [[Creating Own Geometry|create our own geometry]], find out by clicking the redirect link just before. 

## Much better Geometry
For every geometry we have, well most geometry. We have a buffer version which we can use without a cost, only merits of faster rendering and smooth fps.
```js
const geometry = new THREE.BoxBufferGeometry(1, 1, 1, 2, 2, 2); // same parameters
```

We just need to add `Buffer` before `Geometry`


#three