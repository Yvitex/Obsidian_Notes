---
aliases: [applyForce(), applyLocalForce()]
---
# Physics Force
We also could apply some force to the [[Physics World|physics object]] using `applyForce()` and `applyLocalForce()`

Apply local force with accept 2 parameters, which is the direction of the force and the local location of the object
```js
physicsBody.applyLocalForce(new CANNON.Vec3(150, 0, 0), new CANNON.Vec3(0, 0, 0))
```

In this case, we set it to the origin with a 150 force in the positve x axis

Then we have applyForce, which is a force in the negative direction, and it does not need a local point but the physics body position itself which will automatically default into origin
```js
physicsBody.applyForce(new CANNON.Vec3(-0.5, 0, 0), physicsBody.position)
```

If we set the local force outisde the tick function and the apply force to the tick function, then we have this
![[chrome-capture-2022-7-24 (3).gif]]

