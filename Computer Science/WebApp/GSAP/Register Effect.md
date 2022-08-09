# Register Effect 
Is a way to store a [[GSAP Timelines|timeline]] or [[GSAP Programming|tweening]] in a variable to enable reusage. To create one, we need to call this method:
```js
gsap.registerEffect({
	
})
```

Inside this, we will specify a name that will be its identification and an effect property for the actual animation, the function contain 2 parameter which is config, and target object
```js
gsap.registerEffect({
	name: "rainbow",
	effect: (target, config) => {
		
	}	
})
```

Because effect is a function, it must return something
```js
gsap.registerEffect({
	name: "rainbow",
	effect: (target, config) => {
		let split = new SplitText(target, {type: "chars"})
		return gsap.from(split.chars, {y: -100, opacity: 0, stagger: 0.1})
	}	
})
```

we could applit to an element by using `gsap.effects.rainbow()`
```js
gsap.effects.rainbow("h1");
gsap.effects.rainbow("h2");
```

We could also apply it in an order using a [[GSAP Timelines|timeline]]
```js
let animation = gsap.timeline();
animation.add(gsap.effects.rainbow("h1"));
animation.add(gsap.effects.rainbow("h2"));
```

Or in easier syntax,w e could enable the `extendTimeline` property
```js
gsap.registerEffect({
	name: "rainbow",
	extendTimeline: true,
	effect: (target, config) => {
		let split = new SplitText(target, {type: "chars"})
		return gsap.from(split.chars, {y: -100, opacity: 0, stagger: 0.1})
	}	
})
```

Then we could do the application like this
```js
let animation = gsap.timeline();
animation.rainbow("h1").rainbow("h2");
```

We could also chain a timeline inside the effect
```js
gsap.registerEffect({
	name: "rainbow",
	extendTimeline: true,
	effect: (target, config) => {
		let split = new SplitText(target, {type: "chars"})
		let animation = gsap.timeline();
		animation.from(split.chars, {y: -100, opacity: 0, stagger: 0.1})
			.to(split.chars, {color: gsap.utils.wrap(["aqua", "yellow", "pink"]), rotation: 360})
		return animation;
	}	
})
```

And also create a default value, default value is indicated in `config.property`
```js
gsap.registerEffect({
	name: "rainbow",
	extendTimeline: true,
	defaults: {
		y: -100,
		color: ["aqua", "yellow", "pink"]
	},
	effect: (target, config) => {
		let split = new SplitText(target, {type: "chars"})
		let animation = gsap.timeline();
		animation.from(split.chars, {y: config.y, opacity: 0, stagger: 0.1})
			.to(split.chars, {color: gsap.utils.wrap(config.color), rotation: 360})
		return animation;
	}	
})
```

Then we could modify or change it
```js
let animation = gsap.timeline();
animation.rainbow("h1").rainbow("h2", {y: 50}, 0);
```
![[chrome-capture-2022-6-16.gif]]