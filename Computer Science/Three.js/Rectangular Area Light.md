# Rectangular Area Light
This is a rectangular light that only emits light in a single side. 
![[Pasted image 20220818091919.png]]

To do this, we could use
```js
const rectLight = new THREE.RectAreaLight()
```

This will accepts 4 parameters whicha re the color, intensity, height and width
```js
const rectLight = new THREE.RectAreaLight("#00f", 1, 1, 1)
rectLight.position.set(1, 0, 2)
rectLight.lookAt(new THREE.Vector3())
scene.add(rectLight);
```


## Params
- Color
- Intensity
- Height
- Width

