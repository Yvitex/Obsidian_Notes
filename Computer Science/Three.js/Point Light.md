# Point Light
A point object that shines light in all diverging directions.
![[Pasted image 20220818084448.png]]

To do this, just do
```js
const pointLight = new THREE.PointLight("#fff", 0.3);
scene.add(pointLight);
```
![[Pasted image 20220818084539.png]]

We could move this like any other [[Three.js Mesh|mesh]]. 
```js
const pointLight = new THREE.PointLight("#fff", 0.7);
pointLight.position.set(0.5, -0.2, 1)
scene.add(pointLight);
```

![[Pasted image 20220818085429.png]]

We could modify the distance of the light by using the third parameter
```js
cnst pointLight = new THREE.PointLight("#fff", 0.7, 1);
pointLight.position.set(0.5, -0.2, 1)o
scene.add(pointLight);
```

![[Pasted image 20220818085539.png]]


The fourth parameter is the decay or the dim, the higher the number, the lower the light is. 
```js
cnst pointLight = new THREE.PointLight("#fff", 0.7, 1, 2);
pointLight.position.set(0.5, -0.2, 1);
scene.add(pointLight);
```

![[Pasted image 20220818085957.png]]

