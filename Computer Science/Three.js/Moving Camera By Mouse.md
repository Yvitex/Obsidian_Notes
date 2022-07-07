# How to Move Camera By Mouse?
First is we need to know the coordinate of the mouse. We could do this using [[Javascript]] simple event listener function
```js
window.addEventListener('mousemove', (event) =>{
	console.log("x: " + event.clientX + " y:" + "event.clientY");
})
```

In our case, bcause we are working with [[WebGL Renderer|render]], we only need the coordinate inside that render so we must limit the value from 0 - 1 into that render space. We do that by dividing the width and height of the render to the value of the coordinates.  We also have the need to save the value to a variable. 
```js
const cursor = {
	x: 0,
	y: 0
};

const sizes = {
	width: 800,
	height: 600
};

window.addEventListener('mousemove', (event) =>{
	cursor.x = event.clientX / sizes.width;
	cursor.y = event.clientY / sizes.height;

	console.log("x: " + event.clientX + " y:" + "event.clientY");
})
```

And also we could subtract it to one half its value so that the midpoint could be zero rather than the top left part
```js
const cursor = {
	x: 0,
	y: 0
};

const sizes = {
	width: 800,
	height: 600
};

window.addEventListener('mousemove', (event) =>{
	cursor.x = event.clientX / sizes.width - 0.5;
	cursor.y = event.clientY / sizes.height - 0.5;

	console.log("x: " + event.clientX + " y:" + "event.clientY");
})
```

To [[WebGL Renderer|render]] the mvoement of the camera, we also need the boiler plate of the [[Three.js Animations]]. Per movement of mouse, we will change the [[Position (Three.js)|position]] of the  [[Three.js Camera|camera]]
```js
const cursor = {
	x: 0,
	y: 0
};

const sizes = {
	width: 800,
	height: 600
};

window.addEventListener('mousemove', (event) =>{
	cursor.x = event.clientX / sizes.width - 0.5;
	cursor.y = -(event.clientY / sizes.height - 0.5);

	console.log("x: " + event.clientX + " y:" + "event.clientY");
});

const tick = () =>{

	camera.position.x = cursor.x;
	camera.position.y = cursor.y;

	renderer.render(scene, camera);
	window.requestAnimationFrame(tick);
}
```

```ad-Notice
collapse: open
Cursor.y must be negative or else its motion will be disparage to the cursor.x

```

![[chrome-capture-2022-6-5 (6).gif]]

We could applify the effect by miltiplying the camera position by a constant
```js
const cursor = {
	x: 0,
	y: 0
};

const sizes = {
	width: 800,
	height: 600
};

window.addEventListener('mousemove', (event) =>{
	cursor.x = event.clientX / sizes.width - 0.5;
	cursor.y = -(event.clientY / sizes.height - 0.5);

	console.log("x: " + event.clientX + " y:" + "event.clientY");
});

const tick = () =>{

	camera.position.x = cursor.x * 3;
	camera.position.y = cursor.y * 3;

	renderer.render(scene, camera);
	window.requestAnimationFrame(tick);
}
```

![[chrome-capture-2022-6-5 (7).gif]]

For a better looking effect. We could make the motion  only move like a rotation by using the `lookAt` metod
```js
const tick = () =>{

	camera.position.x = cursor.x * 3;
	camera.position.y = cursor.y * 3;
	camera.lookAt(mesh.position);
	renderer.render(scene, camera);
	window.requestAnimationFrame(tick);
}
```

![[chrome-capture-2022-6-5 (8).gif]]

For a  much better rotation, we apply some [[Trigonometric functions]] to the x and z position. One is sin and another is cosine, converging those two forms a circle. The 2 axis we will apply this principle is the x and z as what we need is to rotate the [[Three.js Camera|camera]] horizontally with the same value x. 

```js
const tick = () =>{

	camera.position.x = Math.sin(cursor.x);
	camera.position.z = Math.sin(cursor.x);
	camera.lookAt(mesh.position);
	
	renderer.render(scene, camera);
	window.requestAnimationFrame(tick);
}
```

Because, we only need 1 full revolution, then we apply the principle of [[Pi Revolution]] or simply multiplying the value by 3.1415
```js
const tick = () =>{

	camera.position.x = Math.sin(cursor.x * Math.pi * 2);
	camera.position.z = Math.sin(cursor.x * Math.pi * 2);
	camera.lookAt(mesh.position);
	
	renderer.render(scene, camera);
	window.requestAnimationFrame(tick);
}
```

Then amplify this in accordance to preference.
```js
const tick = () =>{

	camera.position.x = Math.sin(cursor.x * Math.pi * 2) * 2;
	camera.position.z = Math.sin(cursor.x * Math.pi * 2) * 2;
	camera.lookAt(mesh.position);
	
	renderer.render(scene, camera);
	window.requestAnimationFrame(tick);
}
```

For the y position. we simply assign the y coordinate
```js
const tick = () =>{

	camera.position.x = Math.sin(cursor.x * Math.pi * 2) * 2;
	camera.position.z = Math.sin(cursor.x * Math.pi * 2) * 2;
	camera.position.y = cursor.y * 5;
	camera.lookAt(mesh.position);
	
	renderer.render(scene, camera);
	window.requestAnimationFrame(tick);
}
```
![[chrome-capture-2022-6-5 (9).gif]]


But there are some [[Builtin Controls]] in three.hs