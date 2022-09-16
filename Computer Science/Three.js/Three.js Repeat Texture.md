---
aliases: [texture.repeat.x, MirroredRepeatWrapping, RepeatWrapping, texture.wrapS, texture.wrapT, texture.repeat.y]
---
# Repeat Texture
Repeat texture will strech the end pixel of a specified axis. For example
![[Pasted image 20220816060248.png]]

If we set the [[Color Texture]] like this
```js
colorTexture.repeat.x = 2;
colorTexture.repeat.y = 3;
```

![[Pasted image 20220816083056.png]]

This will be the result. In the x axis, we halved the space for the texture to occupu and strech the last pixel to extend to the end. The y axis is now only a third and streched, To make it repeat, as in, if we specify the `repeat` method to 3, then it will have 3 doors, we may have to do this.
```js
colorTexture.repeat.x = 2;
colorTexture.repeat.y = 3;

colorTexture.wrapS = THREE.RepeatWrapping;
```

![[Pasted image 20220816083501.png]]

wrap S will repeat on the sides and T will repeat on the top and bottom. 
```js
colorTexture.repeat.x = 2;
colorTexture.repeat.y = 3;

colorTexture.wrapS = THREE.RepeatWrapping;
colorTexture.wrapT = THREE.RepeatWrapping;
```
![[Pasted image 20220816083557.png]]

Or we could set it into mirror mode using `MirrorRepeatWrapping` from [[Three.js (core)]]
```js
colorTexture.repeat.x = 2;
colorTexture.repeat.y = 3;

colorTexture.wrapS = THREE.MirroredRepeatWrapping;
colorTexture.wrapT = THREE.MirroredRepeatWrapping;
```

![[Pasted image 20220816083656.png]]