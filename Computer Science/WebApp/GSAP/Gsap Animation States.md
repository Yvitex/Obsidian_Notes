---
aliases: [gsap animation controls]
---
# Animation State
- paused()
- reversed()
- timeScale() 
- time()
- progress()

They are all [[Getter and Setter in Java|getter and setter like in java]] but in [[Javascript]]

```js
let controller = gsap.to{...};
```

## Paused
We could see the state of controller if it is paused or not using `paused()`
```js
let controller = gsap.to{...};
console.log(controller.paused());
```

Or set it into a paused state
```js
let controller = gsap.to{...};
controller.paused(true);
```

## Progress
We see the progress of the animation from 0 to 1 ysing this `.progress()`
```js
let controller = gsap.to{...};
console.log(controller.progress());
```

Or start an animation in specified progress
```js
let controller = gsap.to{...};
controller.progress(0.4);
```

## Timescale
This speeds up the animation or get the speed of the animation
```js
let controller = gsap.to{...};
controller.timeScale(2); //speed 2times
console.log(controller.timeScale());
```

## Reversed
Accepts true or false
```js
let controller = gsap.to{...};
controller.reversed(true);
console.log(controller.reversed());
```

## Time
Like `progress()` but is on time unit
```js
let controller = gsap.to{...};
console.log(controller.time());
```

Will only print out one time on the starting animation
```js
let controller = gsap.to{...};
controller.time(3); //reads in seconds
```

## Whole Animation Controls
We could also use this states in tweens. For example
```js
let animation = gsap.to(...);
gsap.to(animation, {progress: 0.5, duration: 3});
```

This will simply goes to halfway to the animation, we could add pause method to stop it right exactly at the progress value
```js
let animation = gsap.to(...);
animation.pause()
gsap.to(animation, {progress: 0.5, duration: 3});
```

This also works the same as `time()` but in seconds. `timeScale()` on the other hand changes the speed of the animation, for example
```js
let animation = gsap.to(...);
gsap.to(animation, {timeScale: 5, delay: 3});
```

This will speed up the animation after 3 seconds.


