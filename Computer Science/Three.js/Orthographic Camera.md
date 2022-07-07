# Orthographic Camera
This is different from [[Perspective Camera]] as it doesn't have perspective and is very parallel to the [[Three.js Scene|scene]].

To set it up, we need more than 2 parameters. They are the `left`, `right`, `top`, `bottom,` `near`, and `far`

```js
const camera = new THREE.OrthographicCamera(-1, 1, 1, -1, 1, 100); // position of edge and near and far
camera.position.x = 2;
camera.position.y = 2;
camera.position.z = 2;
scene.add(camera);
```

We do not need a field of view here.  But the result may become like this, also this is a rotating animation so...
![[Pasted image 20220705150201.png]]

This could be change the changing the size of the [[WebGL Renderer|render]] to be equal to each other forming a square.
```js
const sizes = {
	height: 800, 
	width: 800
}

renderer.setSize(sizes.width, sizes.height);
```

![[Pasted image 20220705150406.png]]

Now this is a square, but we change the shape of the [[WebGL Renderer|render]] it self. Alternatively, we could balance the shape by getting the [[Aspect Ratio]] and multiplying to the sides that will equalize the view of the [[Three.js Camera|camera]]. Because the lenght of the left and right side is shorter, we will multiply the aspect ratio there.
```js
const sizes = {
	height: 800, 
	width: 800
}

const aspectRatio = sizes.width/sizes.height;
const camera = new THREE.OrthographicCamera(-1 * aspectRatio, 1 * aspectRatio, 1, -1, 1, 100);
```

![[Pasted image 20220705150939.png]]

It looks more squarer than before.
