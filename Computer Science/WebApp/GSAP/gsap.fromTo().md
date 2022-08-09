# gsap.fromTo()
This specifies both where it came from, to a specified destination. a combination of bothe [[gsap.to()]] and [[gsap.from()]] that requires 2 objects
```js
gsap.fromTo('.fred', {x: 1000, y: 300, opacity: 0}, {x: 500, y: 250, scale: 3, opacity: 0.7, duration: 3}) // second param == from third param == to
```

![[chrome-capture-2022-6-8 (3).gif]]