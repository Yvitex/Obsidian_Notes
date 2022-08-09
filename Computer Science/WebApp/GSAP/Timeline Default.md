# Timeline Defaults
```js
gsap.timeline()
  .from("#demo", {opacity: 0})
  .from("h1", {x: 100, opacity: 0})
  .from("h2", {x: -50, opacity: 0})
  .from("p", {y: 30, opacity: 0})
  .from("button", {y: 30, opacity: 0})
  .from("#items g", {stagger: 0.1, opacity: 0, scale: 0, transformOrigin: "center center"})
```

```ad-Danger
title: Oh shit fuck
collapse: open
There are too many `opacity: 0`. We could do better than that by using default

```

Simply add a default key inside an object and pass it as a parameter inside the timeline
```js
gsap.timeline({defaults: {opacity: 0, ease: "back"}})
  .from("#demo", {ease: "linear", duration: 0.1})
  .from("h1", {x: 100, duration: 1})
  .from("h2", {x: -50, duration: 1}, "<")
  .from("p", {y: 30}, "-=0.1")
  .from("button", {y: 50}, "-=0.4")
  .from("#items g", {stagger: 0.1, scale: 0, transformOrigin: "center center"}, "-=0.3")
```

We also applied [[Timeline Position]] and [[Ease Property]]
