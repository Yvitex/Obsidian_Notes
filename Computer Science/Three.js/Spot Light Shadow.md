# SpotLight Shadow
![[Pasted image 20220818163419.png]]

Mixing Shadows are terrible idea, 
IN spot light, we do the same activating the `castShadow`

```js
const spotLight = new THREE.SpotLight("#fff", 0.4, 10, Math.PI * 0.3);
spotLight.position.set(0, 2, 2);
spotLight.castShadow = true;
```

To optimize this, what we could do is to lower the `far` and `near`, reduce the camera's `fov`, and reduce the width and height of the `mapSize`
```js
spotLight.shadow.camera.far = 5;
spotLight.shadow.mapSize.width = 1024;
spotLight.shadow.mapSize.height = 1024;
spotLight.shadow.camera.fov = 60;
```

Wifth and height of mapsize must be on power of 2 because of [[Mipmapping]].
Unlike [[Directional Light Shadow]], this utilize a [[Perspective Camera]] 
