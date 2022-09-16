# Directional Light
In [[Three.js Light]], is like the sun in the sky, it produce light in one direction
![[Pasted image 20220818080119.png]]

This is what it looks like. To set this up. 
```js
const directionalLight = new THREE.DirectionalLight("#fff", 0.5);
scene.add(directionalLight);
```

We could move the direction of the light by using this `position.set()`method
```js
const directionalLight = new THREE.DirectionalLight("#fff", 0.5);
directionalLight.position.set(1, 0.25, 0);
scene.add(directionalLight);
```

![[Pasted image 20220818080329.png]]

As we could see, this is not a good light because in the realworld, light bounces, The picture represents a pitch black shadow and must be lightened to show a bouncing light effect
Use [[Ambient Light]] for it, 
![[Pasted image 20220818081118.png]]

