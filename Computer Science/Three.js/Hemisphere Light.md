# Hemisphere Light
Is  a light that glew in 2 sides of the object. Above and Below. ![[Pasted image 20220818083912.png]]

To make this work, we use `HemisphereLight()` class
```js
const hemisphereLight = new THREE.HemisphereLight()
```

This will accept 2 color values and an intensity value
```js
const hemisphereLight = new THREE.HemisphereLight("#f00", "#00f", 0.3);
scene.add(hemisphereLight);
```
![[chrome-capture-2022-7-18.gif]]