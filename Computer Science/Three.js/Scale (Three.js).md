---
aliases: [scale]
---

# Scale
Also utilizes [[Vector3]] functionality enabling us to modify the x, y, z coordinates of an [[Three.js Objects|object]]

Here is an example on how to modify a [[Three.js Mesh|mesh]]

```
mesh.scale.x= 2
mesh.scale.y= 0.5
mesh.scale.z= 0.5
```

we could also use the shortcut method `.set()`

```
mesh.scale.set(2, 0.5, 0.5)
```

![[Pasted image 20220611061603.png]]


#three