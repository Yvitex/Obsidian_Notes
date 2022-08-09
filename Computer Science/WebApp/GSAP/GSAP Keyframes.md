# Gsap Keyframes
## Documentation
Here is the documentation for [keyframes](https://greensock.com/understanding-keyframes)

## Basics
We can create keyframes using percentage in [[GSAP Programming|gsap]].
The basic syntax is
```js
gsap.to{keyframes:{
	
}}
```

This is where we will input some percentage
```js
gsap.to{keyframes:{
	"25%":{y:0},
	"45%":{y:-100},
	"85":{y:0, ease:"bounce"},
	"100%":{x:320, ease:"none"}
	}, duration: 2
}
```

Remember that combination of ease in and ease out forms a curve like a jump, But i prefere a bounce in the end so i use` ease: bounce`, while alldefaults are `ease: power1.out`
![[chrome-capture-2022-6-12 (2).gif]]