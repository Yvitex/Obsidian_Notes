# Timeline Position Basics
![[Position Parameter.rtf]]

```js
gsap.timeline()
	.from("#id", {opacity: 0, duration: 1})
	.from("#title", {scale: 0})
	.from("#freds img", {y: 200, ease: "back", stagger: 0.2})
	.from("#time", {xPercent: 100, ease: "back"})
```

We could create add a delay before the other animation executes by adding a third parameter in the tweens, setting it with the string `"+=1"` or any value in seconds
```js
gsap.timeline()
	.from("#id", {opacity: 0, duration: 1})
	.from("#title", {scale: 0})
	.from("#freds img", {y: 200, ease: "back", stagger: 0.2}, "+=2")
	.from("#time", {xPercent: 100, ease: "back"})
```

Now, before the freds shows up, it will wait 2 seconds after id element title is done in animating itself. The reverse can be said using `"-=1"` which will happen 1 second sooner overlapping some element animation

```js
gsap.timeline()
	.from("#id", {opacity: 0, duration: 1})
	.from("#title", {scale: 0})
	.from("#freds img", {y: 200, ease: "back", stagger: 0.2}, "+=2")
	.from("#time", {xPercent: 100, ease: "back"}, "-=1")
```

Or, if we want the time element to be in sync to the start of the previous element animation, then we use the string `"<"`  to start animating in the same time with the previous animation element. We could also add a value that will create a delay space for it such as `<0.5` which start at the beginning but 0.5 second late than the previous.

```js
gsap.timeline()
	.from("#id", {opacity: 0, duration: 1})
	.from("#title", {scale: 0})
	.from("#freds img", {y: 200, ease: "back", stagger: 0.2}, "+=2")
	.from("#time", {xPercent: 100, ease: "back"}, "<1")
```
