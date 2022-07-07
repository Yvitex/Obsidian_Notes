# FullScreen Mode
Full screen mode for [[Three.js (core)]]. 

The setup is preety simple, i think?
![[Pasted image 20220706053949.png]]

We could set the sizes that will affect the size of the [[WebGL Renderer|renderer]] as well as the [[Aspect Ratio]] of the [[Three.js Camera|camera]] to a dependent value depending on the size of the viewport. We could do this by `window.innerHeight` or width
```js
const sizes = {
	width: window.innerWidth,
	height: window.innerHeight
}

const camera = new THREE.PerspectiveCamera(75, sizes.width / sizes.height, 1, 100);

renderer.setSize(sizes.width, sizes.height)
```

![[Pasted image 20220706054435.png]]

It's well and good but we still have an outline because a default css configuration. Inside our css. we set this
```css
* {
	padding: 0;
	margin: 0;
}
```

We set them to zero to erase background. ![[Pasted image 20220706054654.png]]

Still we have a scroll control, to erase this, we set the overflow to hidden inside the body and html
```css
* {
	padding: 0;
	margin: 0;
}

bodt, html {
	overflow: hidden;
}
```
![[Pasted image 20220706054755.png]]

Now that we erased the scroll control, we next set things up by making the bottom part disappear by setting the [[HTML Canvas]] to fixed value
```css
* {
	padding: 0;
	margin: 0;
}

bodt, html {
	overflow: hidden;
}

.webgl {
	position: fixed;
	top: 0;
	left: 0;
	outline: none; /* set this up to erase highlighting */
}
```

![[Pasted image 20220706055314.png]]

But when we compress the viewport, the thing looks like this
![[Pasted image 20220706055345.png]]

Only half is shown, so to fix this is we try to listen to an eventlistener whenever we resize it,  the canvas will adapt to the size of the browser.

Initially, we update the sizes for the [[Aspect Ratio]] of [[Three.js Camera|camera]] and the [[WebGL Renderer|renderer]] size
```js
const sizes = {
	width: window.innerWidth,
	height: window.innerHeight
}

window.addEventListener('resize', () => {
	// Update Size
	sizes.width = window.innerWidth;
	sizes.height = window.innerHeight;
})
```

Next is to update the canvas `setSize` method so that whenever we change the size of browser, it will adapt
```js
const sizes = {
	width: window.innerWidth,
	height: window.innerHeight
}

window.addEventListener('resize', () => {
	// Update Size
	sizes.width = window.innerWidth;
	sizes.height = window.innerHeight;

	// Update Renderer Size
	renderer.setSize(sizes.width, sizes.height);
})
```

![[chrome-capture-2022-6-6 (4).gif]]

But as you could see, even the [[Three.js Mesh|mesh]] changes in size when we resize it, the problem lies on the [[Three.js Camera|camera]]'s [[Aspect Ratio]]
```js
const sizes = {
	width: window.innerWidth,
	height: window.innerHeight
}

window.addEventListener('resize', () => {
	// Update Size
	sizes.width = window.innerWidth;
	sizes.height = window.innerHeight;

	// Update Camera
	camera.aspect = sizes.width / sizes.height;

	// Update Renderer Size
	renderer.setSize(sizes.width, sizes.height);
})
```

![[Pasted image 20220706060344.png]]

Still does not work yet. every time we update these optical thing, we need to update also the projection matrix of the camera
```js
const sizes = {
	width: window.innerWidth,
	height: window.innerHeight
}

window.addEventListener('resize', () => {
	// Update Size
	sizes.width = window.innerWidth;
	sizes.height = window.innerHeight;

	// Update Camera
	camera.aspect = sizes.width / sizes.height;
	camera.setProjectionMatrix();

	// Update Renderer Size
	renderer.setSize(sizes.width, sizes.height);
})
```

![[chrome-capture-2022-6-6 (5).gif]]

Now that it is full screen, we could set it to a more full screen mode byt applying a dobule click listener that will activate [[Browser FullScreen]]