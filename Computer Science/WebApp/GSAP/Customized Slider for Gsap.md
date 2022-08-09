---
aliases: [gsap onUpdate]
---
# Customized Slider
A slider is an input [[HTML]] element that looks like this
```html
<input id="progressSlider" type="range" min="0" max="1" value="0" step="0.001" />
```

We do this with a min of 0 and max of 1 as our `.progress()` value can only be a range of 0 to 1 inclusive.
We also add a div element of numbers where we will input the value of the progress bar based on time. Just remember that the step value must be small enough and the type is range
```html
<div id="time">0.00</div>
```

We use the [[Smart Button|special technique in querySelector]] to mount the element to a variable
```js
let progressSlider = select("#progressSlider");
```

To change the animation based on the slider, we could create a event listener for that element that when we input a value, it will customize the `.progress()` which is one of the  [[Gsap Animation States]]

```js
progressSlider.addEventListener("input", function(){
	animation.progress(progressSlider.value);
})
```

We may also want to pause the entire animtion while we are moving the slider, we could say
```js
progressSlider.addEventListener("input", function(){
	animation.progress(progressSlider.value).pause();
})
```
![[chrome-capture-2022-6-12 (7).gif]]

We should also change the textcontent in the button in a variable called pause.
```js
progressSlider.addEventListener("input", function(){
	animation.progress(progressSlider.value).pause();
	pause.textContent = "play";
})
```

## onUpdate
To move the slider automatically while it is playing, we could utilize another property of [[GSAP Programming|tweening]] called `onUpdate`
```js
let animation = gsap.to("#herman", { duration:6, ease:"none",
  motionPath:{
    path:"#motionpath",
    align:"#herman"
  },
  onUpdate: animationUpdate, // Animation Update is a function to be called
  onComplete: () => pause.innerHTML = "play"
});
```

We create the function by ourselves
```js
function animationUpdate(){
	
}
```

The logic is, we set the value of the slider equals to the progress
```js
function animationUpdate(){
	progressSlider.value = animation.progress();
}
```

Also we change the value of the number value with id of time with the value of time in seconds.
```js
let time = select("#time");

function animationUpdate(){
	progressSlider.value = animation.progress();
	time.textContent = animation.time();
}
```

This will print out a lot of decimal places so we need to use `toFixed()`
```js
let time = select("#time");

function animationUpdate(){
	progressSlider.value = animation.progress();
	time.textContent = animation.time().toFixed(2); // set to 2 decimal place
}
```
![[chrome-capture-2022-6-12 (8).gif]]

