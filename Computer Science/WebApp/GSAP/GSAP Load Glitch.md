---
aliases: [gsap loader function]
---
# How to fix the load glitch?
This is caued by [[CSS]] loading before the [[Javascript]], i think?
![[chrome-capture-2022-6-8 (13).gif]]

Well we could set the opacity of the [[CSS]] to 0 then animate it so that the glitch won't show though all of it won;t show forever. What we will do is to set the `visibility` to hidden
```css
#demo{
	visibility: hidden;
	/*Other styling*/
}
```

Inside the js. 
```js
gsap.timeline({defaults: {opacity: 0, ease: "back"}})
  .from("#demo", {ease: "linear", duration: 0.1})
  .from("h1", {x: 100, duration: 1})
  .from("h2", {x: -50, duration: 1}, "<")
  .from("p", {y: 30}, "-=0.1")
  .from("button", {y: 50}, "-=0.4")
  .from("#items g", {stagger: 0.1, scale: 0, transformOrigin: "center center"}, "-=0.3")
```

Actually, let's translate it using a variable reference
```js
let controls = gsap.timeline({defaults: {opacity: 0, ease: "back"}})

controls.from("#demo", {ease: "linear", duration: 0.1})
  .from("h1", {x: 100, duration: 1})
  .from("h2", {x: -50, duration: 1}, "<")
  .from("p", {y: 30}, "-=0.1")
  .from("button", {y: 50}, "-=0.4")
  .from("#items g", {stagger: 0.1, scale: 0, transformOrigin: "center center"}, "-=0.3")
```

We could set it on an event listener called `"load"`
```js
window.addEventListener("load", () => {
	controls.from("#demo", {ease: "linear", duration: 0.1})
	  .from("h1", {x: 100, duration: 1})
	  .from("h2", {x: -50, duration: 1}, "<")
	  .from("p", {y: 30}, "-=0.1")
	  .from("button", {y: 50}, "-=0.4")
	  .from("#items g", {stagger: 0.1, scale: 0, transformOrigin: "center center"}, "-=0.3")
})
```

We will add in the demo id a new property called `autoAlpha` which when set to 0, will translate the element from `visibility: hidden` and `opacity: 0` to `visibility: initial` and `opacity: 1`
![[chrome-capture-2022-6-8 (14).gif]]


See, no glitch.