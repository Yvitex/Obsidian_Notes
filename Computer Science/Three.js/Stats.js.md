---
aliases: []
---
# Stats.js
[Stats.js](https://github.com/mrdoob/stats.js/) is a library that measures the performance of a program in different ways such as FPS etc.

![[Pasted image 20220914022839.png]]

Install the library
```bash
$ npm install stats.js
```

Import it 
```js
import Stats from 'stats.js'
```

Instantiate this import then choose the 0 index as default measurement
```js
const stats = new Stats()
stats.newPanel(0)
```

Add then this instance to the [[DOM]]
```js
document.body.addChild(stats.dom)
```

Next is to `begin` and `end` this object inside the [[Three.js Animations]] tick
```js
const tick = () => {
	stats.begin()

	//...

	stats.end()
	window.requestAnimationFrame(tick)
}
```

![[Pasted image 20220914024034.png]]


we could then [[Disable the FPS Limit of Chrome]] because it will limit the performance to only 60fps maximum. 

---
###### Related: 
[[Three.js Animations]], [[Three.js Performance Tips]], 
###### Tags:
#three #javascript #libraries