# Transform Origin
![[chrome-capture-2022-6-8(neo).gif]]

If you ever found the animation of small items weird because of how it scale up, we could actually change where it will original using `transformOrigin` property
```js
gsap.timeline()
  .from("h1", {x: 100, opacity: 0})
  .from("h2", {x: -50, opacity: 0})
  .from("p", {y: 30, opacity: 0})
  .from("button", {y: 30, opacity: 0})
  .from("#items g", {stagger: 0.1, opacity: 0, scale: 0})
```

We'll just add that property
```js
gsap.timeline()
  .from("h1", {x: 100, opacity: 0})
  .from("h2", {x: -50, opacity: 0})
  .from("p", {y: 30, opacity: 0})
  .from("button", {y: 30, opacity: 0})
  .from("#items g", {stagger: 0.1, opacity: 0, scale: 0, transformOrigin: "center center"})
```

![[chrome-capture-2022-6-8 (13).gif]]

Here is the [documentation](https://www.w3schools.com/cssref/css3_pr_transform-origin.asp) for the [[CSS]] property
The values it accepts are
- right
- left
- center
- %
In both x and y and only length in z

We could make this a little more readable... read [[Timeline Default]] to learn how to remove redundant opacity code
