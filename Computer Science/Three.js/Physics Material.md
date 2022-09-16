---
aliases: [CANNON.Material(), CANNON.ContactMaterial()]
---
# Physics Material
We could create physics material using `Material()` constructor. We could have several materials like metal, concrete, jelly or plastic, here we will use only 2
```js
const plasticMaterials = new CANNON.Material("plastic")
const concreteMaterials = new CANNON.Material("concrete")
```

The collision fo these materials will be our main focus, create a `ContactMaterial()` instance based on those materials
```js
const plasticConcreteMaterial = new CANNON.ContactMaterial(
	plasticMaterials,
	concreteMaterials,
	{
		
	}
)
```

This will accept 3 arguments, the 2 being the materials instance, and the next are the physics options. Here we will use the `friction` which is the friction and the `restitution ` which is the amount of bounce. 
```js
const plasticConcreteMaterial = new CANNON.ContactMaterial(
	plasticMaterials,
	concreteMaterials,
	{
		friction: 0.1,
		restitution: 0.7
	}
)
```

Add this material tot he world using `addContactMaterial`
```js
world.addContactMaterial(plasticConcreteCollision)
```

Apply those materials to the physics object using `material` property
```js
const physicsBody = new CANNON.Body({
    mass: 1,
    position: new CANNON.Vec3(0, 3, 0),
    shape: physicsShape,
    material: plasticMaterials
})

const physicalPlane = new CANNON.Body()
physicalPlane.addShape(planeShape)
physicalPlane.mass = 0
physicalPlane.material = concreteMaterials
physicalPlane.quaternion.setFromAxisAngle(
    new CANNON.Vec3(-1, 0, 0),
    Math.PI * 0.5
)
```

![[chrome-capture-2022-7-24 (2).gif]]


We could also make a default physics material that will be applied to everything
This will have only 1 material applied to everything
```js
const defaultMaterials = new CANNON.Material("default")

const defaultContactMaterial = new CANNON.ContactMaterial(
    defaultMaterials,
    defaultMaterials,
    {
        friction: 0.1,
        restitution: 0.7
    }
)

world.addContactMaterial(defaultContactMaterial)
```

Then set it to the meshes
```js
const physicsShape = new CANNON.Sphere(0.5)
const physicsBody = new CANNON.Body({
    mass: 1,
    position: new CANNON.Vec3(0, 3, 0),
    shape: physicsShape,
    material: defaultMaterials
})

world.addBody(physicsBody)

const planeShape = new CANNON.Plane()
const physicalPlane = new CANNON.Body()
physicalPlane.addShape(planeShape)
physicalPlane.mass = 0
physicalPlane.material = defaultMaterials
physicalPlane.quaternion.setFromAxisAngle(
    new CANNON.Vec3(-1, 0, 0),
    Math.PI * 0.5
)

world.addBody(physicalPlane)
```

Or we could simply apply it to everything by adding this code
```js
world.defaultContactMaterial = defaultContactMaterial
```
