# GSAP SplitText
## Documentation
Documentation for [SplitText](https://greensock.com/docs/v3/Plugins/SplitText?ref=6234)

## Basics
Available on [[GSAP Programming|gsap]]
Unfortunately, this is only available with club plugins. 
```html
<div class="classer">
	<h1>Letter by letter animation with GSAP</h1>
</div>
```

Install GSap core and SplitText
```url
https://cdnjs.cloudflare.com/ajax/libs/gsap/3.10.4/gsap.min.js
https://assets.codepen.io/16327/SplitText3.min.js
```

Create a timeline
```js
let split;
let animation = gsap.timeline({});
```

To prevent [[GSAP Load Glitch]], create a function
```js
let split;
let animation = gsap.timeline({});

function init(){

}

window.addEventListener("load", init);
```

Set the class to visible alpha. Classer class is visibility hidden
```js
let split;
let animation = gsap.timeline({});

function init(){
	gsap.set(".classer", autoAlpha(1));
}

window.addEventListener("load", init);
```

Instantiate the SplitText class, it will accept 2 parameter which is the html element contianing text, then the object that contian the type of split it will have, in our case, `chars` type
```js
let split;
let animation = gsap.timeline({});

function init(){
	gsap.set(".classer", autoAlpha(1));
	split = new SplitText("h1", {type: "chars"});
}

window.addEventListener("load", init);
```

`split` variable will contain what needs to be animated, we could now animate it
```js
let split;
let animation = gsap.timeline({});

function init(){
	gsap.set(".classer", {autoAlpha: 1});
	split = new SplitText("h1", {type: "chars"});
	animation.from(split.chars, {opacity: 0, y: 50, ease: "back", stagger: 0.1})
}

window.addEventListener("load", init);
```
![[chrome-capture-2022-6-12 (1).gif]]


