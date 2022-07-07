# How to group objects
Sometimes, we want to move or [[Transform Object]]s in a group altogether. We could easily do that using `Three.Group()` method.
```js
const group = new THREE.Group();
scene.add(group);
```

We will add this group to our scene.

When we create a [[Three.js Mesh|mesh]] which is a combination of [[Three.js Geometry|geometry]] and materials. We could add this mesh not to the scene but to the group
```js
const object1 = new THREE.Mesh(new THREE.BoxGeometry(1, 1, 1), new THREE.MeshBasicMaterial({color: "red"}));

group.add(object1);

const object2 = new THREE.Mesh(new THREE.BoxGeometry(1, 1, 1), new THREE.MeshBasicMaterial({color: "green"}));

object3.position.x = -3;
group.add(object2);

const object3 = new THREE.Mesh(new THREE.BoxGeometry(1, 1, 1), new THREE.MeshBasicMaterial({color: "blue"}));

object3.position.x = 3;
group.add(object3);
```

Now, we could move the meshes altogether by
```js
group.position.y = 1;
```

