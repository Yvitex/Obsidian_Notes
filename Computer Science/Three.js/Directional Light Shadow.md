# Directional Light Shadow
The final thing to do is to enable the cast of shadow by the light itself, for example is [[Directional Light]]
```js
directionalLight.castShadow = true;
```

![[Pasted image 20220818151723.png]]


This is kind of hazy shadow. The problem is, when we console log `directionalLight.shadow`, the mapSize of the shadowmap is so small therefore having low resolution, we need to double it. 
![[Pasted image 20220818152142.png]]

```js
directionalLight.shadow.mapSize.height = 1024;
directionalLight.shadow.mapSize.width = 1024;
```

![[Pasted image 20220818152247.png]]


We could further optimize it by shortening the range of the [[Directional Light]]. 

Lucky for us, we have a camera property inside [[Directional Light]] `shadow` property, we could use it to create a [[Three.js Ligh tHelpers|camera helper]]. This will visualize the direction of light

```js
const cameraHelper = new THREE.CameraHelper(directionalLight.shadow.camera);
scene.add(cameraHelper)
```

![[Pasted image 20220818152840.png]]

See that it is too long and unused, welp lucky for us, the camera in the [[Directional Light]] have a `far` and `near` function.  We could cut excess camera in here which is a kind of [[Orthographic Camera]]
```js
directionalLight.shadow.camera.far = 6;
```

![[Pasted image 20220818153127.png]]

![[Pasted image 20220818155242.png]]

The [[Directional Light]] `shadow.camera` property also have top, left, bottom and right position. what we could do is to compress the size of the rendering camera in order to optimize the scope of the shadow map
```js
directionalLight.shadow.camera.top = 2;
directionalLight.shadow.camera.left = -2;
directionalLight.shadow.camera.right = 2;
directionalLight.shadow.camera.bottom = -2;
```

![[Pasted image 20220818155413.png]]

Now, the shadow is more sharp in circumfernce. We could blur the sides using the [[Directional Light]] `shadow.radius` property
```js
directionalLight.shadow.radius = 10;
```
![[Pasted image 20220818155655.png]]


We coudl change also the type of the shadow using the [[WebGL Renderer|renderer]] shadowmap
```js
renderer.shadowMap.type = THREE.PCFSoftShadowMap;
```

![[Pasted image 20220818160144.png]]
