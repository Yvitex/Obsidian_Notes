# Killing Tweens
Or simply stopping and element from animating or [[GSAP Programming|tweening]]

```js
let animation = gsap.to(".blue, .pink", {scale: 0.2, rotation: 360, repeat: -1, yoyo: true, ease: "power1.out", duration: 2})
```

We have 2 classes that are being animated, to stop a single class from animating, we use `killTweenOf`
First, we create a button that will execute the function containing the kill tweens
```js
let button = document.querySelector("#button");

button.addEventListener("click", kill);

function kill(){
	gsap.killTweensOf(".blue");
}
```

This will stop entire ly the animation of class blue element. For a specific kill in properties, we could add another string parameter to do this.
```js
let button = document.querySelector("#button");

button.addEventListener("click", kill);

function kill(){
	gsap.killTweensOf(".blue", "scale");
}
```
![[chrome-capture-2022-6-12 (9).gif]]

