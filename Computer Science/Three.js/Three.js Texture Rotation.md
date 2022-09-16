# Texture Rotation
We could do a simple texture rotation by using the `texture.rotation` property
```js
colorTexture.rotation = Math.PI * 0.25;
```

We know that Pi is half rotation, PI x 0.25 is PI/4 .
![[Pasted image 20220816084607.png]]

This will rotate in the bottom left part of the [[Three.js Mesh|mesh]] which is (0, 0). What we could do is change the origin point to center
```js
colorTexture.center.x = 0.5;
colorTexture.center.y = 0.5;
```

Moving it by 0.5 will make it go towards the center.
![[Pasted image 20220816085011.png]]
