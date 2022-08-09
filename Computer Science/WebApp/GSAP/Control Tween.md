# Controlling Tween in GSAP
```js
gsap.to('.fred', {x: 400, duration: 3})
```

This will mvoe [octopops](https://gogoanime.lu/category/ansatsu-kyoushitsu-tv-2nd-season) in x positon by 400 pixels. But we could set this into default so that it won't move on load using `paused` [[GSAP Property]]
```js
gsap.to('.fred', {x: 400, duration: 3, paused: true})
```

To control it, we must set this into a variable as a reference
```js
let controls = gsap.to('.fred', {x: 400, duration: 3, paused: true})
```

We could have a button like this
```html
<button id="play">play</button>
```

We could make it functional by getting the element
```js
document.getElementById("play")
```

Then adding an event to it, 
```js
document.getElementById("play").onclick 
```

Then setting it equals to a function 
```js
document.getElementById("play").onclick = () => {}
```

They way to control this is by getting the variable then adding the `play()` method
```js
let controls = gsap.to('.fred', {x: 400, duration: 3, paused: true})
document.getElementById("play").onclick = () => controls.play();
```

Other methods include
- `controls.play()`
- `controls.pause()`
- `controls.reverse()`
- `controls.restart()`


Related: [[gsap.from()]], [[gsap.fromTo()]]