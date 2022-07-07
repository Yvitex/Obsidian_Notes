# Gsap.to()
We could vreate a simple animation by using this
```js
gsap.to('.star', {x: 100, duration: 3});
```

But ut does not only affect a single element but multiple as long as they have the star class. 
It could also manipulate multiple properties at once
```js
gsap.to('.star', {x: 100, rotation: 360, fill: "yellow", duration: 3});
```

And also separate the animation time of each element using `stagger` property
```js
gsap.to('.star', {x: 100, rotation: 360, fill: "yellow", stagger: 1, duration: 3});
```

One thing to note is that when we don't apply any duration, it will default into 500 ms, we could change the default value such as
```js
gsap.to('.fred', {x: innerWidth / 2, y: innerHeight / 2, rotation: 360, scale: 3})
```
![[chrome-capture-2022-6-8.gif]]

Which is too fast, we add the default as in
```js
gsap.defaults({duration: 3});
gsap.to('.fred', {x: innerWidth / 2, y: innerHeight / 2, rotation: 360, scale: 3})
```
![[chrome-capture-2022-6-8 (1).gif]]

Elements can be a class or id, and can even be an [[HTML]] element. 

Remember that inside [[Javascript]], we are using camel casing

![[Basic Tween.rtf]]

See the available [[GSAP Properties]] 