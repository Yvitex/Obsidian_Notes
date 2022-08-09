---
aliases: [special technique in querySelector, gsap onComplete]
---
# Smart Button
A more advance way to [[Control Tween]], it is a button that could play, restart and pause depending on the [[Gsap Animation States]]

## Basics
Constructing this is very simple. Just kidding though.
First, we create a event listener for the button. We use this special technique in query selector
```js
let select = (e) => {document.querySelector(e)}
```

This will enable us to use select vaiable like a function, because it is indeed a function or an arrow function. Here are some [information](https://www.geeksforgeeks.org/different-ways-of-writing-functions-in-javascipt/) regarding it
```js
let select = e => document.querySelector(e);

let button = select("#button");
```

Now add the event listener [[Javascript]]
```js
button.addEventListener("click", () => {
	
})
```

For an instance that we have this animation [[GSAP Programming|tweening]]
```js
let animation = gsap.to("#herman", { duration:6, ease:"none",
  motionPath:{
    path:"#motionpath",
    align:"#herman"
  }});

button.addEventListener("click", () => {
	
})
```

Then we could check weather the animation is paused or not, if it is paused, when we click the button it will play, if it is playing, then it will pause. We'll use the ternary expression because it is easier
```js
let animation = gsap.to("#herman", { duration:6, ease:"none",
  motionPath:{
    path:"#motionpath",
    align:"#herman"
  }});

button.addEventListener("click", () => {
	animation.paused() ? animation.play() : animation.pause();
})
```

We also change the name into play or pause vice versa depending on the state of animation. We do this using `textContent` attribute
```js
let animation = gsap.to("#herman", { duration:6, ease:"none",
  motionPath:{
    path:"#motionpath",
    align:"#herman"
  }});

button.addEventListener("click", () => {
	animation.paused() ? animation.play() : animation.pause();
	animation.paused() ? button.textContent = "play" : button.textContent = "paused";
})
```
![[chrome-capture-2022-6-12 (4).gif]]

The problem is, we cannot restart the animation, to do this is to create an if else statement that will detect if the animation is done or not, then when we click, it will restart the animation
```js
let animation = gsap.to("#herman", { duration:6, ease:"none",
  motionPath:{
    path:"#motionpath",
    align:"#herman"
  }});

button.addEventListener("click", () => {
	animation.paused() ? animation.play() : animation.pause();
	animation.paused() ? button.textContent = "play" : button.textContent = "paused";
	if(animation.progress() == 1){
		animation.restart();
	}
})
```

The problem will be help on the button display, it will not change text to pause or play properly when we restart the animation. In our [[Control Tween]], we have a propertu called `onComplete` that will execute once the animation is done. We will use this to reset the `textContent` of button to play
```js
let animation = gsap.to("#herman", { duration:6, ease:"none",
  motionPath:{
    path:"#motionpath",
    align:"#herman"
  },
	onComplete: () => button.textContent = "play";
});

button.addEventListener("click", () => {
	animation.paused() ? animation.play() : animation.pause();
	animation.paused() ? button.textContent = "play" : button.textContent = "paused";
	if(animation.progress() == 1){
		animation.restart();
	}
})
```
![[chrome-capture-2022-6-12 (5).gif]]

As we could see, we have a problem on displayin the text inside the button. The problem is we print the string before we restart, we must restart first before printing the string.
```js
let animation = gsap.to("#herman", { duration:6, ease:"none",
  motionPath:{
    path:"#motionpath",
    align:"#herman"
  },
	onComplete: () => button.textContent = "play";
});

button.addEventListener("click", () => {
	animation.paused() ? animation.play() : animation.pause();
	if(animation.progress() == 1){
		animation.restart();
	}
	animation.paused() ? button.textContent = "play" : button.textContent = "paused";
})
```
![[chrome-capture-2022-6-12 (6).gif]]

