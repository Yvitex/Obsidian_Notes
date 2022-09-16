# Point Light Shadow
Like [[Spot Light Shadow]], this have a [[Perspective Camera]] view but with total of 6 renders of shadow maps.

We set the castShadow to true
```js
const pointLight = new THREE.PointLight("#fff", 0.3);
pointLight.castShadow = true;
pointLight.position.set(-1, 1, 0);
```

To optimize, we reduce the  `far` and `near` then camera's mapSize `width` and `height`

```js
pointLight.shadow.mapSize.width = 1024;
pointLight.shadow.mapSize.height = 1024;
pointLight.shadow.camera.far = 6;
pointLight.shadow.camera.near = 0.1;
```

