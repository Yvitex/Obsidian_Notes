# Callbacks
Are such thing such as [[Smart Button|gsap onComplete]] and [[Customized Slider for Gsap|gsap onUpdate]] which calls a function in a specified animation state

Here are the other callbacks
- onComplete
- onUpdate
- onRepeat
- onStart
- onReverseComplete


```js
gsap.to(".fred", {scale: 3, duration: 2, onComplete: someFunction});
```

We create a function that will be called `onComplete`
```js
gsap.to(".fred", {scale: 3, duration: 2, onComplete: someFunction});

function someFunction(){
	console.log("Execuuted");
}
```

We could also pass parameters using `onCompleteParams`, remember that it will only accept an array
```js
gsap.to(".fred", {scale: 3, duration: 2, onComplete: someFunction, onCompleteParams: ["Hello"]});

function someFunction(message){
	console.log("Execuuted " + message);
}
```

We could also create an arrowFunction
```js
gsap.to(".fred", {scale: 3, duration: 2, onComplete: () => console.log("Executed")})
```

Keep in mind that in an arrow function, the `this` keyword does not work the same as in function declaration
```js
gsap.to(".fred", {scale: 3, duration: 2, onComplete: someFunction, onCompleteParams: ["Hello"]});

function someFunction(message){
	console.log(this); // Refers to the Tween
}
```

This refers to the tween, we could also get the tarfet element of the tween using the `this.target()` method
```js
gsap.to(".fred", {scale: 3, duration: 2, onComplete: someFunction, onCompleteParams: ["Hello"]});

function someFunction(message){
	console.log(this.target()); // Will return an array of elements
}
```

We could also log the properties of that tween like scale, duration etc as the this keywork refer to the [[GSAP Programming|tweening]] itself
```js
gsap.to(".fred", {scale: 3, duration: 2, onComplete: someFunction, onCompleteParams: ["Hello"]});

function someFunction(message){
	console.log(this.scale()); // Will return an array of elements
}
```

```ad-Attention
title: This doesn't work every time
collapse: open
But of course, inside a class, this thing won't be the same as the `this` keyword will refer to the instance of the class or an object.


```
