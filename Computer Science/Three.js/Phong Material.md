# Phong Material
Is like [[Lambert Material]] but with light reflectivty and specular. 

```js
const material = new THREE.MeshPhongMaterial();
```

![[Pasted image 20220816164808.png]]

As we could see in the picture, it have some form of a denser light in one spot. We could increase this reflectivity using the `shininess` property
```js
const material = new THREE.MeshPhongMaterial();
material.shininess = 100;
```

![[Pasted image 20220816164926.png]]

Amd change the color of the shine using `specular` property
```js
const material = new THREE.MeshPhongMaterial();
material.shininess = 100;
material.specular = new THREE.Color("blue");
```
![[Pasted image 20220816165124.png]]
