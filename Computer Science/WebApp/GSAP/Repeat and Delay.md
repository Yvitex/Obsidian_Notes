# Repeat and Delay
If you don't want the elements to mvoe at the same time, we could provide a delay in seconds such as
```js
gsap.to('.fred_1', {x: 500, duration: 3, delay: 1}) // will wait for 1 second before executing
gsap.to('.fred_2', {x: 500, duration: 3, delay: 2}) // will wait for 2 seconds before executing
```

We could also repeat the animation using repeat properties with value specifying the amount of times we execute it such as
```js
gsap.to('.fred_1', {x: 500, duration: 3, repeat: 2, delay: 1}) // will wait for 1 second before executing
gsap.to('.fred_2', {x: 500, duration: 3, repeat: 2, delay: 2}) // will wait for 2 seconds before executing
```

![[chrome-capture-2022-6-8 (4).gif]]

This is also known as teleporting octopus. To make things more appealing, we could set yoyo to true
```js
gsap.to('.fred_1', {x: 500, duration: 3, repeat: 2, yoyo: true, delay: 1}) 
gsap.to('.fred_2', {x: 500, duration: 3, repeat: 2, yoyo: true, delay: 2})
```

`repeat: 2` in this case is an individual movement. 1 backward then 1 forward is repeat: 2. To make this infinite, we could set `repeat` to -1
```js
gsap.to('.fred_1', {x: 500, duration: 3, repeat: -1, yoyo: true, delay: 1}) 
gsap.to('.fred_2', {x: 500, duration: 3, repeat: -1, yoyo: true, delay: 2})
```

![[chrome-capture-2022-6-8 (5).gif]]