# gsap.utils.wrap
## Documentation
This is the documentation for the [wrap()](https://greensock.com/docs/v3/GSAP/UtilityMethods/wrap())

## Basics
This is a method that will alternate through a [[GSAP SplitText]]
First create a [[GSAP Load Glitch|gsap loader function]]
```js
gsap.registerPlugin(SplitText);

function init(){

}

window.addEventListener("load", init);
```

Create a basic timeline and instantiate the SplitText
```js
gsap.registerPlugin(SplitText);

let animation = gsap.timeline();
function init(){
	let split = new SplitText("h1", {type: "chars"});
	
}

window.addEventListener("load", init);
```

because we are using a loader, our class container contains a visibility hidden, set the class to visible after load
```js
gsap.registerPlugin(SplitText);

let animation = gsap.timeline();
function init(){
	gsap.set(".wrapper", {autoAlpha: 1});
	let split = new SplitText("h1", {type: "chars"});
	
}

window.addEventListener("load", init);
```

Now animate using `gsap.utils.wrap()`, this will accept an array of values that will be applied to an interval.
```js
gsap.registerPlugin(SplitText);

let animation = gsap.timeline();
function init(){
	gsap.set(".wrapper", {autoAlpha: 1});
	let split = new SplitText("h1", {type: "chars"});
	animation.from(split.chars, {
								y: gsap.utils.wrap([-100, 100]);
								opacity: 0,
								stagger: {each: 0.05, from: "center"}
									})
}

window.addEventListener("load", init);
```
![[chrome-capture-2022-6-12 (10).gif]]

Add color effect
```js
gsap.registerPlugin(SplitText);

let animation = gsap.timeline();
function init(){
	gsap.set(".wrapper", {autoAlpha: 1});
	let split = new SplitText("h1", {type: "chars"});
	animation.from(split.chars, {
								y: gsap.utils.wrap([-100, 100]);
								opacity: 0,
								stagger: {each: 0.05, from: "center"}
									})
			.to(split.chars, {color: gsap.utils.wrap(["blue", "green", "aqua"])})

window.addEventListener("load", init);
```

![[chrome-capture-2022-6-12 (11).gif]]

Add others
```js
gsap.registerPlugin(SplitText);

let animation = gsap.timeline();
function init(){
	gsap.set(".wrapper", {autoAlpha: 1});
	let split = new SplitText("h1", {type: "chars"});
	animation.from(split.chars, {
								y: gsap.utils.wrap([-100, 100]);
								opacity: 0,
								stagger: {each: 0.05, from: "center"}
									})
			.to(split.chars, {color: gsap.utils.wrap(["blue", "green", "aqua"])})
			.to(split.chars, {y: gsap.utils.wrap([50, 40, 30, -50, -40, -30])})
window.addEventListener("load", init);
```

![[chrome-capture-2022-6-12 (12).gif]]



