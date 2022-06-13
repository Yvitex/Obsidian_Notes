---
aliases: [render, renderer]
---

# How to use the WebGL Renderer?
WebGL renderer, renders our scene and objects. It is a necessary part to print out objects in the web browser

First of all, we need to create an [[HTML Canvas]] where we can render the components.
`<canvas class="webgl"></canvas>`

Next is to import that element inside Javascript
`const canvas = document.querySelector(".webgl")`

Now, instantiate the webgl renderer object and pass in the canvas as its object parameter

```
const renderer = new THREE.WebGLRenderer({
	canvas: canvas
})
```

However, the size might be incorrect to the viewport

![[Pasted image 20220605052014.png]]

Therefore, what we need to do is to set the size in accordance to the [[Three.js Camera|camera]]'s aspect ratio.

```
const sizes = {
	width: 800,
	height: 600
}

renderer.setSize(sizes.width, sizes.height)
```

Now we can render the [[Three.js Scene|scene]] with the [[Three.js Camera|camera]]

`renderer.render(scene, camera)`


## Activity
![[Pasted image 20220605060834.png]]



