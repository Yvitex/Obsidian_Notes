# Ambient Light
Ambient light are kinds of light that hits the surface everywhere in all directions or Omnidirectional. ![[Pasted image 20220818075238.png]]

It does not produce shadows or whatnot. 
To create this. just include this to the scene, `AmbientLight()` will accept a color property and intensity
```js
const ambientLight = new THREE.AmbientLight("#fff", 0.5);
scene.add(ambientLight);
```

Or use this
```js
const ambientLight = new THREE.AmbientLight();
ambientLight.color = new THREE.Color("#fff");
ambientLight.intensity = 0.5;
scene.add(ambientLight);
```

In this form of light, all sides are hit by a light
![[Pasted image 20220818075649.png]]

