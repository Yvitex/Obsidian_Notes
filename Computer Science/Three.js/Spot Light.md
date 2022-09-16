# Spot Light
Is like a flashlight that has a circular light area
![[Pasted image 20220818093208.png]]

```js
const flashLight = new THREE.SpotLight()
```

This will accept 5 parameters which are the color, intensity, distance, angle, penumbra and decay

```js
const flashLight = new THREE.SpotLight("#0f0", 1, 10, Math.PI * 0.1, 1, 1)
scene.add(flashLight)
```

To move where te light is pointing, we cannot use [[Rotation (Three.js)|rotation()]] or [[Rotation (Three.js)|lookAt()]] method but instead, what we move is the `target` property 

```js
const flashLight = new THREE.SpotLight("#0f0", 1, 10, Math.PI * 0.1, 1, 1)
flashlight.target.position.x = -1;
scene.add(flashLight)
```

This won't work yet, the target is not exisiting within the scene, so we add it
```js
const flashLight = new THREE.SpotLight("#0f0", 1, 10, Math.PI * 0.1, 1, 1)
flashLight.target.position.x = -1;
scene.add(flashLight, flashLight.target)
```

![[Pasted image 20220818111538.png]]

## Params
- Color
- Intensity : strength of light
- Distance : how far will the light goes
- Angle : The radius or how big the circle is, increase the `0.1` value with PI will enlarge it
- Penumbra : increasing this will make the circumference sharp
- Decay : just put 1 in here. 

