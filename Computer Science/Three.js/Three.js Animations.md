# Animation Basics
There are 3 ways we could do a smple [[Three.js Mesh|mesh]] animation

## Using Delta Time
First is we need to understand the use of `window.requestAnimationFrame()`. This method is used when trying to call a function repeatedly. We use it like this.
```js
const tick = () => {
	console.log("tick");
	window.requestAnimationFrame(tick); // we call the function tick again here
}

tick();
```

![[Pasted image 20220705053220.png]]

We could use this to make an animation. But first, we must not forget to add the renderer each time we will call the function, 
```js
const tick = () => {
	mesh.position.y += 0.01;
	renderer.render(scene, camera);
	window.requestAnimationFrame(tick); // we call the function tick again here
}

tick();
```
![[chrome-capture-2022-6-5.gif]]

But this isn't enough. Each computer have each own FPS speed, meaning different computers could have different movement, so what we will do is to calculate the [[Delta Time]] and multiply it to the value position. 

In this example, I will change for a moment the [[Transform Object|transformation]] animation to [[Rotation (Three.js)|rotation]]. In our [[Javascript]] programming, `Date.now` is a [[UNIX Time]] scale. ![[Pasted image 20220705055951.png]]
```js
let previousTime = Date.now();

const tick = () => {
	const currentTime = Date.now();
	const deltaTime = currentTime - previousTime;
	previousTime = currentTime // update the previous time
	
	mesh.rotation.y += 0.001 * deltaTime;
	renderer.render(scene, camera);
	window.requestAnimationFrame(tick); // we call the function tick again here
}

tick();
```
![[chrome-capture-2022-6-5 (1).gif]]

Is we print the [[Delta Time]].![[Pasted image 20220705060330.png]]

## Using Clock
We could get the similar thing using a Clock object specially when we are just transofrming something in a loop
```js
const clock = new THREE.Clock()

const tick = () =>{
	let time = clock.getElapsedTime();
	mesh.rotation.y = time;
	renderer.render(scene, camera);
	window.requestAnimationFrame(tick);
}
```
![[chrome-capture-2022-6-5 (2).gif]]

If we print out the value of `.getElapsedTime()`
```js
const clock = new THREE.Clock();
const tick = () =>{
	let time = clock.getElapsedTime();
	console.log(time);
	window.requestAnimationFrame(tick);
}
```

![[Pasted image 20220705060828.png]]


We could also use [[Trigonometric functions]] in animation such as
```js
const clock = new THREE.Clock()

const tick = () =>{
	let time = clock.getElapsedTime();
	mesh.position.x = Math.sin(time);
	renderer.render(scene, camera);
	window.requestAnimationFrame(tick);
}
```

![[chrome-capture-2022-6-5 (3).gif]]

Or we could do.
```js
const clock = new THREE.Clock()

const tick = () =>{
	let time = clock.getElapsedTime();
	mesh.position.x = Math.sin(time);
	mesh.position.y = Math.cos(time);
	renderer.render(scene, camera);
	window.requestAnimationFrame(tick);
}
```
![[chrome-capture-2022-6-5 (4).gif]]

## Using GSAP
[[GSAP Programming|GSAP]] or green sock is a libray for animting a website, so therefore we need to install if before usage
```shell
$ npm install gsap@3.5.1
```

We want the specfic version of [[GSAP Programming|gsap]] but we could also do the latest version.
Next is to import it inside the source code
```js
import gsap from 'gsap';
```

Of course, this is the case when we are using [[Babel]] or modern browser. The function we need to use is `gsap.to()`
```js
gsap.to(mesh.position, {duration: 1, delay: 1, x: 1});
gsap.to(mesh.position, {duration: 1, delay: 2, y: 1});
```

`gsap.to()` accepts 2 parameter, first is the [[Three.js Objects|object]] to be animated and then a object with 3 necessary properties such as duration, delay and [[Position (Three.js)|position]]. This won't work independtly because we still need to render it repeatedly like a machinegun screenshot
```js
gsap.to(mesh.position, {duration: 1, delay: 1, x: 1});
gsap.to(mesh.position, {duration: 1, delay: 2, y: 1});

const tick = () =>{
	renderer.render(scene, camera);
	window.requestAnimationFrame(tick);
} // this is a necessary function
```
