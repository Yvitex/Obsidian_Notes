---
aliases: [position]
---

# Position
Can be moved by using the xyz coordinates. Unit values are arbitrary so we don;t need to think about it. We could set the position of the objects such as [[Three.js Mesh|mesh]] and [[Three.js Camera|camera]] using this code

```
mesh.position.x = 1
```

where we set the x coordinate into 1, In other words, we are moving the mesh to the right by unit 1. We could do it along with other xyz coordinate

```
mesh.position.x = 1
mesh.position.y = 0.5
```
![[Pasted image 20220611060650.png]]

The shortcut to this is by using `set()` method
```
mesh.position.set(1, 0.5) #we could add another parameter for z. 
```

Keep in mind that moving the meshes will only work before [[WebGL Renderer|render]]ing the [[Three.js Camera|camera]]. It won't work after.

## Vector3
Position inherits from [[Vector3]], setting aside the ability to change the values of each coordinate, we could use every method that vector3 has to offer. Here are some of the examples

### Measuring length
#####  From Object to Center
This will measure the distance between the center of the [[Three.js Scene|scene]] and the [[Three.js Mesh|mesh]]
```
console.log(mesh.position.length())
```
Output: 1.118033988749895
##### From Object to Object
Measure the distance from [[Three.js Mesh|mesh]] to the [[Three.js Camera|camera]]
```
console.log(mesh.position.distanceTo(camera.position))
```
Output: 3.2015621187164243

### Repositioning
`.normalize()` will set the length of the [[Three.js Objects|object]] to the center of the [[Three.js Scene|scene]]
```
mesh.position.normalize()
console.log(mesh.position.length())
```
Output: 0.9999999999999999

![[Pasted image 20220611061237.png]]

We could also move the [[Three.js Camera|camera]]

![[Pasted image 20220611061341.png]]




