# Ease Property
Is one of the [[GSAP Property]]. We could refer to what type of ease to use in [[Ease Visualizer for GSAP]]
For now, here are the example
```js
gsap.to('.fred', {x: 500, duration: 3, ease: back})
```

This will make the object extend over the specified x value and returns. We could also specify the amount of overshoot it will take by making this a function
```js
gsap.to('.fred', {x: 500, duration: 3, ease: back(6)})
```
![[chrome-capture-2022-6-8 (8).gif]]

The second element code is
```js
gsap.to('.fred_2', {x: 500, duration: 3, ease: linear})
```

Meaning it does not have any eases. There are many other more eases such as bounce, elastic etc
```js
gsap.to('.fred', {x: 500, duration: 3, ease: bounce})
```

![[chrome-capture-2022-6-8 (9).gif]]

We could also change if it is bounce in, our bounce out. For example
```js
gsap.to('.fred', {x: 500, duration: 3, ease: bounce.in})
```

![[chrome-capture-2022-6-8 (10).gif]]

It could even be both in and out
```js
gsap.to('.fred', {x: 500, duration: 3, ease: bounce.inOut})
```

![[chrome-capture-2022-6-8 (11).gif]]