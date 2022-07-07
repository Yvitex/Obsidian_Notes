# Perspective Camera
To set it up, we only need 2 parameters which is [[Field of View]] and [[Aspect Ratio]]
```js
const sizes = {
	height: 800,
	width: 600
}

const camera = new THREE.PerspectiveCamera(75, sizes.width/ sizes.height);

scene.add(camera);
```

We could also add the `far` and `near` parameter.
```js
const sizes = {
	height: 800,
	width: 600
}

const camera = new THREE.PerspectiveCamera(75, sizes.width/ sizes.height, 1, 100);

scene.add(camera);

```

Near and far corresponds to how close or far could the camera see. If it is in the scope not greater than 100 and less than 1, then the object is deleted from the camera unless they move closer or farther. 

```ad-Danger
title: No Extreme Values plsss...
collapse: open
In case of near and far, we must not set it to 0.0001 and 9999999 as it may cause a z-fighting

```
![[chrome-capture-2022-6-5 (5).gif]]

Overlapping goku vs vegeta fight.