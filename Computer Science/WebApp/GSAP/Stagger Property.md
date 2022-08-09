# GSAP Stagger property
```js
gsap.to('#fred img', {y: -50, stagger: 1})
```

This will cause a delay between each execution for 1 second. This doesn't need a duration period
![[chrome-capture-2022-6-8 (6).gif]]

Inside the stagger properties, nested an object with `each`, `amount`, and `from` properties
When we say `each`, its practically the same as the default above
```js
gsap.to('#fred img', {y: -50, stagger: {each: 1}}) // 1 second delay each
```

Replace this with amount, each delayed execution is shared in that whole value
```js
gsap.to('#fred img', {y: -50, stagger: {amount: 1}}) // execution are shared in that 1 second
```

`from` will dictate from where the animation should start
```js
gsap.to('#fred img', {y: -50, stagger: {amount: 1, from: "center"}}) 
```

![[chrome-capture-2022-6-8 (7).gif]]

Here are the other values available for `from`
- center
- edges
- end
- start

