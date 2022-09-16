# Fogs
It will blur [[Three.js Mesh|mesh]] that is far away from the camera and clears when we go near

```js
const fog = new THREE.Fog("#262837", 1, 15)
scene.fog = fog
```

Will accept 3 parameters such as color, near and far. 

![[Pasted image 20220819100425.png]]

