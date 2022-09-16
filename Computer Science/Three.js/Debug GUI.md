# How to Create a Debugger User Interface
There are many library to consider such as
- [dat.gui](https://github.com/dataarts/dat.gui)
- [control-panel](https://github.com/freeman-lab/control-panel)
- [ControlKit](https://github.com/automat/controlkit.js/)
- [Guify](https://github.com/colejd/guify)
- [Oui](https://github.com/wearekuva/oui)

## DAT gui
First is to import the library
```shell
$ npm i dat.gui
```

```js
import * as dat from 'dat.gui';
```

Instantiate an object using the dat class
```js
const gui = new dat.GUI();
```

To add something as a controller GUI, we use `.add()` method. Here is an example for [[Transform Object|transforming object]] in [[Three.js Mesh|mesh]]
```js
gui.add(mesh.position, 'y');
```

It is not weird. mesh.position is the object, and y is the  specific name for the value. The specific name is the one that is changed. ![[chrome-capture-2022-6-6 (7).gif]]

We could make a slider by adding a parameter, but it is more efficient to create a chain method for this.
```js
gui.add(mesh.position, 'y').min(-3).max(3).step(0.001);
```

This will indicate the minimum and maximum value of the slider as well as the amount of change when we use it. Also we could change the name using the `.name()` method. ORganizing it...
```js
gui
	.add(mesh.position, 'y')
	.min(-3)
	.max(3)
	.step(0.001)
	.name("elevation")
```

![[chrome-capture-2022-6-6 (8).gif]]

Boolean is easier. we just need to add it and that's it. For example is when we are editing the wireframe
```js
gui
	.add(material, 'wireframe');
```

Wireframe is a boolean value from material object
![[chrome-capture-2022-6-6 (9).gif]]

How about adding colors. then it is different, we use `addColor()`. But in our [[Three.js Materials|materials]], there is no way to access the color property as it only an instace of the color class. Which means, we create our own parameter to solve the problem
```js
const parameter = {
	color: 0xff0000,
}
```

This will be added to the gui, as in
```js
gui
	.addColor(parameter, 'color')
```
![[chrome-capture-2022-6-6 (10).gif]]

It does not work, to make this work, for every changes we made, we update the color of the box.
```js
const parameter = {
	color: 0xff0000,
}

gui
	.addColor(parameter, 'color')
	.onChange(() => {
		material.color.set(parameter.color); // this is how we will update the color
	})
```

![[chrome-capture-2022-6-6 (11).gif]]


Now, how to add a specific function. Because, again, we do not have a way to access this custom function directly, we create our own object so, remember the [[GSAP Programming|gsap]] [[Three.js Animations]]?
```js
const parameter = {
	color: 0xff0000,
	spin: () => {
		gsap.to(mesh.rotation, {duration: 1, y: 10});
	}
}
```

Now to add this is very simple
```js
const parameter = {
	color: 0xff0000,
	spin: () => {
		gsap.to(mesh.rotation, {duration: 1, y: 10});
	}
}

gui
	.add(parameter, spin)
```

But there is a problem in our spin logic, it only spin once. It is because we the position of the rotation is already equal to the specified rotation so it does not move. We replace this by adding 10 rather than equal 10
```js
const parameter = {
	color: 0xff0000,
	spin: () => {
		gsap.to(mesh.rotation, {duration: 1, y: mesh.rotation.y + 10}),
	}
}

gui
	.add(parameter, spin);
```
![[chrome-capture-2022-6-6 (12).gif]]

We could also set the width of our control by saying in our parameter
```js
const gui = new dat.GUI({closed: true, width: 400})
```

Closed true means the controler is closed by default
![[Pasted image 20220706191658.png]]


To set this up inside and change a function, what we could do is to call `onFinishChange`
```js
gui.add(parameters, "count").min(100).max(1000).step(10).onFinishChange(generateGalaxy)
gui.add(parameters, "size").min(0.01).max(0.2).step(0.01).onFinishChange(generateGalaxy)
```

