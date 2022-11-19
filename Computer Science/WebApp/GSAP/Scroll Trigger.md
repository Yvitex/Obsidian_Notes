# Scroll Trigger
Another feature of [[GSAP Programming|gsap]] that could execute an animation when the user enters a viewport

To use this, import this CDN
```js
https://cdnjs.cloudflare.com/ajax/libs/gsap/3.3.0/ScrollTrigger.min.js
```

Then [[Register Effect]] called scorllTrigger
```js
gsap.registerPlugin(ScrollTrigger)
```

If we have this [[GSAP Programming|tweening]] 
```js
gsap.from(".herman", {
  duration:10, x:"-50vw", rotation:-360, ease:"linear")
```

we could add the scrollTrigger property
```js
gsap.from(".herman", {
  duration:10, x:"-50vw", rotation:-360, ease:"linear",
  scrollTrigger: {
	  trigger: ".herman"
  }
```

The trigger key will make the class as the marker that when it hits a certain viewport level, it will execute, to visualize this. use the marker keyword
```js
gsap.from(".herman", {
  duration:10, x:"-50vw", rotation:-360, ease:"linear",
  scrollTrigger: {
	  trigger: ".herman",
	  markers: true
  }
```

![[Pasted image 20220811053156.png]]

We could modify its position using the `start` and `end` key
```js
gsap.from(".herman", {
  duration:10, x:"-50vw", rotation:-360, ease:"linear",
  scrollTrigger: {
	  trigger: ".herman",
	  markers: true,
	  start: "top 75%",
	  end: "bottom 25%"
  }
```

![[Pasted image 20220811053405.png]]


We could control these interaction between the markers and the class using the `toggleAction` key. This will control the enter, the leave, the re enter and releave actions
```js
gsap.from(".herman", {
  duration:10, x:"-50vw", rotation:-360, ease:"linear",
  scrollTrigger: {
	  trigger: ".herman",
	  markers: true,
	  start: "top 75%",
	  end: "bottom 25%"
	  toggleActions: "restart pause play reset"
  }
```


To make an item move based on the progress of the scroll, we could use the key word `scrub` and set it to true or 1 for an additional easing in a [[GSAP Timelines|timeline]]
```js
let tl = gsap.timeline({scrollTrigger:{
	trigger:".carWrapper",
	start:"top 50%",
	end:"bottom 50%",
	markers:true,
	scrub:1,
}})
```

![[chrome-capture-2022-7-11.gif]]

And we could apply a `pin` in order to make the object vertically stay in place

```js
let tl = gsap.timeline({scrollTrigger:{
	trigger:".carWrapper",
	start:"top 50%",
	end:"bottom 50%",
	markers:true,
	scrub:1,
	pin: true
}})
```

![[chrome-capture-2022-7-11 (1).gif]]

