---
aliases: []
---
# Three.js
We could add some [[HTML]] to add some interaction to the [[Three.js (core)]]. Here, what we want is a button where when we hover, it will output some text,

The first step of course is to create the [[HTML]] content. We want a way to select them all and select them individually so we need 2 class for the container
```html
<div class="point point-0">
	<div class="label">1</div>
	<div class="text">Lorem ipsum, dolor sit amet consectetur</div>
</div>
```

This won't show up if we wrote this after the [[HTML Canvas]] because it is below the viewport. What we could do is to modify the position to center using absolute positioning
```css
.point {
    position: absolute;
    top: 50%;
    left: 50%;
}
```

![[Pasted image 20220915131501.png]]

We want to hide the text so set it into `display: none` 
```css
.point .text{
    display: none;
}
```

Now we modify the number to have a transparent dark circular background 
```css
.point .label{
    position: absolute;
    width: 40px;
    height: 40px;
    top: -20px;
    left: -20px;
    background-color: #00000077;
    border: 1px solid #ffffff77;
    color: white;
    border-radius: 50%;
    font-family: Helvetica, Arial, sans-serif;
    text-align: center;
    display: flex;
    justify-content: center;
    align-items: center;
    font-weight: 100;
    font-size: 14px;
}
```
![[Pasted image 20220915132454.png]]


Next is to edit the styling for the text class, remove the `display: none` property and repalce it with `opacity: 0` so that it could be animated later
```css
.point .text{
    /* display: none; */
    position: absolute;
    left: -120px;
    top: 30px;
    width: 200px;
    background-color: #00000077;
    color: white;
    line-height: 1.3em;
    font-family: Helvetica, Arial, sans-serif;
    font-weight: 100;
    font-size: 14px;
    padding: 20px;
    border-radius: 4px;
    
    opacity: 0;
}
```

![[Pasted image 20220915134522.png]]

Now we hide it again and reveal it when the mouse hover to the label class
```css
.point:hover .text{
    opacity: 1;
}
```

Put a transition to the text class so that it smoothens the animation

```css
.point .text{
    /* display: none; */
    position: absolute;
    left: -120px;
    top: 30px;
    width: 200px;
    background-color: #00000077;
    color: white;
    line-height: 1.3em;
    font-family: Helvetica, Arial, sans-serif;
    font-weight: 100;
    font-size: 14px;
    padding: 20px;
    border-radius: 4px;
    opacity: 0;
    transition: opacity 0.3s;
}
```

Still, the labels appear in the point class, meaning even if we don't hover, it will still reveal itself when it's close enough to an invisible container. We could disable the 
```css
.point .text{
    /* display: none; */
    position: absolute;
    left: -120px;
    top: 30px;
    width: 200px;
    background-color: #00000077;
    color: white;
    line-height: 1.3em;
    font-family: Helvetica, Arial, sans-serif;
    font-weight: 100;
    font-size: 14px;
    padding: 20px;
    border-radius: 4px;
    opacity: 0;
    transition: opacity 0.3s;
    pointer-events: none;
}
```

If we hover to the label, we could change the interaction of the mouse to help
```css
.point .label{
    position: absolute;
    width: 40px;
    height: 40px;
    top: -20px;
    left: -20px;
    background-color: #00000077;
    border: 1px solid #ffffff77;
    color: white;
    border-radius: 50%;
    font-family: Helvetica, Arial, sans-serif;
    text-align: center;
    display: flex;
    justify-content: center;
    align-items: center;
    font-weight: 100;
    font-size: 14px;
    cursor: help;
}
```

![[chrome-capture-2022-8-15s.gif]]

We want to hide this label when it is supposed to be hidden so what we could do is to apply the scale in the label to 0 so that it is hidden by default
```css
.point .label{
	/*...*/
	transform: scale(0, 0);
    transition: transform 0.3s;
}
```

Then we could revert back to normal the size once it is supposed to do that. Here we add the class visible to the point and then the label class will scale up
```css
.point.visible .label{
    transform: scale(1, 1);
}
```

We could test using the dev tools. Press the cls, select the element and then add the visible class
![[Pasted image 20220915140836.png]]

We could now test it if it is working
![[chrome-capture-2022-8-15 (3).gif]]


We want to move this point in the scene when we move the [[Three.js Camera|camera]]. But how could we do that?
First create an array of points that will represent this label class. Each point must contain an object that has a [[Vector3]] position and an [[HTML]] element
```js
const points = [
    {
        position: new THREE.Vector3(1.55, 0.3, -0.6),
        element: document.querySelector('.point-0')
    }
]
```

We will put the actual movement inside the [[Three.js Animations]] tick function. Create a for loop that will traverse the items in the points
```js
for(let point of points) {
  
}
```

We want to fetch the position of the points without changing the original value. We could do that using `clone()`
```js
for(let point of points) {
  const screenPosition = point.position.clone()
}
```

The Idea is that we are converting the location of the [[Vector3]] associated to the point into an actual 2d position based on the camera's [[Field of View]]. What we could do is to use the `project()` property.
![[Pasted image 20220916025220.png]]

```js
for(let point of points) {
  const screenPosition = point.position.clone()
  screenPosition.project(camera)
}
```

`project()` method will output the value in a normalized formed. We need to convert it somehow to adapt into the sizes of the viewport. Multiply the x and y value with the sizes width and height then divide it by 2.
```js
for(let point of points) {
  const screenPosition = point.position.clone()
  screenPosition.project(camera)
  const translateX = screenPosition.x * sizes.width * 0.5
  const translateY = -screenPosition.y * sizes.height * 0.5
}
```

Now, access the element in the points array then modify the styling using the css using `transform`. we should always use transform in animation as it is more performant than ordinaty CSS animation

```js
for(let point of points) {
  const screenPosition = point.position.clone()
  screenPosition.project(camera)
  const translateX = screenPosition.x * sizes.width * 0.5
  const translateY = -screenPosition.y * sizes.height * 0.5
  point.element.style.transform = `translate(${translateX}px, ${translateY}px)`
}
```
![[chrome-capture-2022-8-16.gif]]


The problem now is that it won;t disappear when it is behind the [[Three.js Mesh|mesh]]. What we could do is to use a [[Raycaster and MouseEvents|raycaster.setFromCamera()]] method

![[Pasted image 20220916031621.png]]

We will use the raycaster to test if the point is intesecting with something and if yes, then we will test if the [[Three.js Mesh|mesh]] have lower length from the [[Three.js Camera|camera]] and to the point [[Vector3]]. 
```js
const rayCaster = new THREE.Raycaster()
```

Inside the tick function, we will test perframe the intersection from the raycaster. Set the ray caster using the [[Raycaster and MouseEvents|raycaster.setFromCamera()]] method, this will make the raycaster originate from the [[Three.js Camera|camera]], we will use the normalized coordinate from the `project(camera)` position.
```js
for(let point of points) {
  const screenPosition = point.position.clone()
  screenPosition.project(camera)
  const translateX = screenPosition.x * sizes.width * 0.5
  const translateY = -screenPosition.y * sizes.height * 0.5
  point.element.style.transform = `translate(${translateX}px, ${translateY}px)`

  rayCaster.setFromCamera(screenPosition, camera)
}
```

Next is we detect the intersections happening in the [[Three.js RayCaster|THREE.Raycaster()]]. In our case, we want to test all items in the scene so
```js
for(let point of points) {
  const screenPosition = point.position.clone()
  screenPosition.project(camera)
  const translateX = screenPosition.x * sizes.width * 0.5
  const translateY = -screenPosition.y * sizes.height * 0.5
  point.element.style.transform = `translate(${translateX}px, ${translateY}px)`

  rayCaster.setFromCamera(screenPosition, camera)
  const intersects = rayCaster.intersectObjects(scene.children, true)
}
```

The second parameter will let us iterate over childrens so that no stone is left unturned. We want to test is there is an intersection or not, if there is, then don't show the label by removing the visible class. If not, then we will add that class
```js
for(let point of points) {
  const screenPosition = point.position.clone()
  screenPosition.project(camera)
  const translateX = screenPosition.x * sizes.width * 0.5
  const translateY = -screenPosition.y * sizes.height * 0.5
  point.element.style.transform = `translate(${translateX}px, ${translateY}px)`

  rayCaster.setFromCamera(screenPosition, camera)
  const intersects = rayCaster.intersectObjects(scene.children, true)
  if(intersects.length === 0) {
	  point.element.classList.add('visible')
  }
  else{
	  point.element.classList.remove('visible')
  }
}
```

The problem is, it will only become visible when something is not intersecting with it, but if there is, then it will not show up no matter what. What we could do is to check the distance of the first array of the intersection and compare it to the distance from the point to the camera. We would place the code if the length of the intersection is not 0.

Create 2 variables regarding the 2 distances
```js
for(let point of points) {
  const screenPosition = point.position.clone()
  screenPosition.project(camera)
  const translateX = screenPosition.x * sizes.width * 0.5
  const translateY = -screenPosition.y * sizes.height * 0.5
  point.element.style.transform = `translate(${translateX}px, ${translateY}px)`

  rayCaster.setFromCamera(screenPosition, camera)
  const intersects = rayCaster.intersectObjects(scene.children, true)
  if(intersects.length === 0) {
	  point.element.classList.add('visible')
  }
  else{
	    const firstArrayDistance = intersects[0].distance
        const pointDistance = point.position.distanceTo(camera.position)
  }
}
```

Check if the firstarray is nearer than the point distance. If true, then don't show the element, if false, then add the visible class to the element
```js
for(let point of points) {
  const screenPosition = point.position.clone()
  screenPosition.project(camera)
  const translateX = screenPosition.x * sizes.width * 0.5
  const translateY = -screenPosition.y * sizes.height * 0.5
  point.element.style.transform = `translate(${translateX}px, ${translateY}px)`

  rayCaster.setFromCamera(screenPosition, camera)
  const intersects = rayCaster.intersectObjects(scene.children, true)
  if(intersects.length === 0) {
	  point.element.classList.add('visible')
  }
  else{
	    const firstArrayDistance = intersects[0].distance
        const pointDistance = point.position.distanceTo(camera.position)
        if(firstArrayDistance < pointDistance || firstArrayDistance > 10) {
            point.element.classList.remove('visible')
        }
        else{
            point.element.classList.add('visible')
        }
  }
}
```

![[chrome-capture-2022-8-16 (1).gif]]


We could improbe it more, notice that when we start the application, it immaediately reveals the [[HTML]] element before the [[Three.js Scene|scene]] even loaded. What we could do is to make the loop, if and only if the scene is ready and wait for 3s after that.

Create a variable that will be our boolean switcher. Default to false
```js
const sceneReady = false
```

More the points loop inside the tick function inside an if statement that will execute only if the scene is ready
```js
if(sceneReady){
	for(let point of points) {
	  const screenPosition = point.position.clone()
	  screenPosition.project(camera)
	  const translateX = screenPosition.x * sizes.width * 0.5
	  const translateY = -screenPosition.y * sizes.height * 0.5
	  point.element.style.transform = `translate(${translateX}px, ${translateY}px)`
	
	  rayCaster.setFromCamera(screenPosition, camera)
	  const intersects = rayCaster.intersectObjects(scene.children, true)
	  if(intersects.length === 0) {
		  point.element.classList.add('visible')
	  }
	  else{
			const firstArrayDistance = intersects[0].distance
			const pointDistance = point.position.distanceTo(camera.position)
			if(firstArrayDistance < pointDistance || firstArrayDistance > 10) {
				point.element.classList.remove('visible')
			}
			else{
				point.element.classList.add('visible')
			}
	  }
	}
}
```

Now, inside the [[Three.js Loading Manager]], Loaded callback
```js
const loadingManager = new THREE.LoadingManager(
	// Loaded
	() =>
	{
		// ...
		window.setTimeout(() => {
			sceneReady = true
		}, 3000)
	
	},
	// Progress
	() => {
		 // ...
	}
)
```

We could add more points in the [[HTML]]
```html
<div class="point point-0">
	<div class="label">1</div>
	<div class="text">Lorem ipsum, dolor sit amet consectetur</div>
</div>

<div class="point point-1">
	<div class="label">2</div>
	<div class="text">Lorem ipsum, dolor sit amet consectetur</div>
</div>

<div class="point point-2">
	<div class="label">3</div>
	<div class="text">Lorem ipsum, dolor sit amet consectetur</div>
</div>
```

```js
const points = [
    {
        position: new THREE.Vector3(1.55, 0.3, -0.6),
        element: document.querySelector('.point-0')
    },
    {
        position: new THREE.Vector3(0.5, 0.8, -1.6),
        element: document.querySelector('.point-1')
    },
    {
        position: new THREE.Vector3(1.6, -1.3, -0.7),
        element: document.querySelector('.point-2')
    },
]
```

![[chrome-capture-2022-8-16 (2).gif]]

# Metatags
###### Related: 
[[HTML]], [[Three.js (core)]], [[DOM]]
###### Tags:
#three #html #dev-tools 

---
