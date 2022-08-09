---
aliases: [timeline]
---
# TimeLines
Why timelines? Because it provides a sequence of animation without specofying actually a delay. In short, it helps in the timing of animation
![[Basic Timeline.rtf]]

We could create timelines by simply setting a `gsap.timeline()` method. We will attach any tweens such as [[gsap.to()]] or [[gsap.from()]] to that method in a chain
```js
gsap.timeline()
	.from("id", {opacity: 0, duration: 1})
```

Will start with 0 opacity then appears.
```js
gsap.timeline()
	.from("#id", {opacity: 0, duration: 1})
	.from("#title", {scale: 0})
	.from("#freds img", {y: 200, ease: "back", stagger: 0.2})
```

After the opacity appears, the title will scale up from zero. After that, freds will appear from below with [[Ease Property]] of back which means overthrow with [[Stagger Property]] effect. 

```js
gsap.timeline()
	.from("#id", {opacity: 0, duration: 1})
	.from("#title", {scale: 0})
	.from("#freds img", {y: 200, ease: "back", stagger: 0.2})
	.from("#time", {xPercent: 100, ease: "back"})
```

`xPercent` is a [[GSAP Property]] where it will get the measurement of the element object then move it the same measurement to the x axis. 
![[chrome-capture-2022-6-8 (12).gif]]

Now, to modify the [[Timeline Position]]
