# Physics Performance Optimization
![[chrome-capture-2022-7-24 (4).gif]]

The problem in our physics is that, the objects are tested each time if the other object is colliding with it or not  eventhough the items are far away from each which is too much for the cpu, What we could do is to change the physics algorithm or what we call the Broadphase

Here are some f the broadphase
- `NaiveBroadphase` - default - test every object against each other
- `GridBoradphase` - high performance, divides the axis in grids and only the items that are near each other or in the same grid are tested, But if a fast moving body collides with it, it will just pass through
- `SAPBroadphase` - the better one. Just use it

To use this we just need to modify the property of the  [[Physics World]]
```js
world.broadphase = new CANNON.SAPBroadphase(world)
```

we pass the world itself as the argument.
The next thing we may want is to turn off the test when the body is at rest. And to do this is just to add this code
```js
world.allowSleep = true
```

