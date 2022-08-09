# Timeline Controls
Controls in [[GSAP Timelines|timeline]] is the same with basic [[Control Tween]]s. But with additional feature such as jumping from animation to animation.
```js
gsap.timeline()
	.from("#id", {opacity: 0, duration: 1})
	.from("#title", {scale: 0})
	.from("#freds img", {y: 200, ease: "back", stagger: 0.2})
	.from("#time", {xPercent: 100, ease: "back"})
```

We could create buttons that will act as our controller
```html
<div id="nav">
    <button id="play">play</button>
    <button id="pause">pause</button>
    <button id="reverse">reverse</button>
    <button id="restart">restart</button>
    <button id="test">test</button> <!-- new feature -->
</div>
```

We could create a reference like this
```js
let controls = gsap.timeline()
	.from("#id", {opacity: 0, duration: 1})
	.from("#title", {scale: 0})
	.from("#freds img", {y: 200, ease: "back", stagger: 0.2})
	.from("#time", {xPercent: 100, ease: "back"})
```

Then set the controllers like this
```js
document.getElementById("play").onclick= () => controls.play();
document.getElementById("pause").onclick= () => controls.pause();
document.getElementById("reverse").onclick= () => controls.reverse();
document.getElementById("restart").onclick= () => controls.restart();
```

The new feature is for jumping. But first we must add a marker in where we wll jump in the [[GSAP Timelines|timeline]]
```js
let controls = gsap.timeline()
	.from("#id", {opacity: 0, duration: 1})
	.from("#title", {scale: 0})
	.from("#freds img", {y: 200, ease: "back", stagger: 0.2})
	.add("test")
	.from("#time", {xPercent: 100, ease: "back"})
```

The function we will use is `controls.play("test")`
```js
document.getElementById("play").onclick= () => controls.play();
document.getElementById("pause").onclick= () => controls.pause();
document.getElementById("reverse").onclick= () => controls.reverse();
document.getElementById("restart").onclick= () => controls.restart();
document.getElementById("test").onclick= () => controls.play("test");
```