---
aliases: [window.scrollY, three.js parallax]
---
# Scroll Base animation
Another trick for [[Three.js Animations]]. 
First thing to do is to disable the `overflow: hidden` property in [[CSS]] body and html. then set the canvas to `fixed` then set set the background of the whole document to any color. 

## Preparation
After these css tweaks, set the [[WebGL Renderer]] to alpha true
```js
const renderer = new THREE.WebGLRenderer({
    canvas: canvas,
    alpha: true,
})
```

This is just to set the cavas background into transparent and enable scrolling to the html

Create [[Three.js Mesh|mesh]] to your liking
```js

const material = new THREE.MeshToonMaterial({color: parameters.color})

const mesh1 = new THREE.Mesh(
    new THREE.TorusBufferGeometry(1, 0.4, 16, 60),
    material
)

const mesh2 = new THREE.Mesh(
    new THREE.ConeBufferGeometry(1, 2, 32),
    material
)

const mesh3 = new THREE.Mesh(
    new THREE.TorusKnotBufferGeometry(0.8, 0.35, 100, 16),
    material
)

scene.add(mesh1, mesh2, mesh3)
```

![[Pasted image 20220823115736.png]]

The text above is [[HTML]]. The actual meshes is not visible, it is because the material we use are the type that requires light. Create a light to your own liking if you use a light required material. In our case, ill use [[Directional Light]]
```js
const directionalLight = new THREE.DirectionalLight("#fff", 0.7)
directionalLight.position.set(1, 1, 0)
scene.add(directionalLight)
```

![[Pasted image 20220823120001.png]]

We only have 2 values, the dark shade the light in the color of mesh, to expand this selection we must use a [[Gradient Texture]]. 

![[3.jpg]]

This picture must only be a dot but it is a gradient with 3 pixels
![[Pasted image 20220823120406.png]]

We could apply this using [[Three.js Texture Loader]] to the material
```js
const material = new THREE.MeshToonMaterial({color: parameters.materialColor})
material.gradientMap = gradientTexture
```
![[Pasted image 20220823120654.png]]

Now set the [[Magnification Filter]] to near to avoid this [[Mipmapping]] tragedy
```js
gradientTexture.magFilter = THREE.NearestFilter
gradientTexture.mipmaps = false
```

![[Pasted image 20220823120918.png]]


Move them to a distance and you know how, then animate is using the tick funtion
```js
mesh1.position.y = - distance * 0
mesh2.position.y = - distance * 1
mesh3.position.y = - distance * 2

const meshArray = [mesh1, mesh2, mesh3] // store the mesh inside an array for animation

const tick = () =>
{
    const elapsedTime = clock.getElapsedTime()
    
    // Rotation Animation
    for (let meshes of meshArray) {
        meshes.rotation.x = elapsedTime * 0.1
        meshes.rotation.y = elapsedTime * 0.12
    }
    
    // Render
    renderer.render(scene, camera)
    // Call tick again on the next frame
    window.requestAnimationFrame(tick)
}
```

That's it for the preparation, the real thing starts now

## Scroll Events
The first thing you need to do is to get the value of the `scrollY`
```js
let scrollY = window.scrollY
```

But it won't update automatically, it will only executes one time so what we could do is to create an [[Javascript|Js event listener]]
```js
window.addEventListener("click", () => {
	scrollY = window.scrollY
})
```

We could set it then as the position of the camera
```js
window.addEventListener("click", () => {
	scrollY = window.scrollY
	camera.position.y = scrollY
})
```
![[chrome-capture-2022-7-23 (3).gif]]

The problem is that it scrolls too much and in the wrong direction, multiply it by negative 1 to make the direction right. And because the mesh are separated by 4 units, we could divide it by the size height of the viewport then multi-ply it by the units separation which is 4
```js
window.addEventListener("click", () => {
	scrollY = window.scrollY
	camera.position.y = - scrollY / sizes.height * distance // sizes.height corresponds to inner viewport height
})
```


## Parallax
Now that we have a fix, we could then create a parallax effect, we could do this by using `mousemove` event listener. Save it into a object with 2 parameter, x and y just like vector2
```js
const mouseCoor = {
    x: 0,
    y: 0
}

window.addEventListener("mousemove", (event) => {
    mouseCoor.x = event.clientX / sizes.width - 0.5
    mouseCoor.y = -(event.clientY / sizes.height - 0.5)
}
```

This is already a normalize version where when you move the mouse, it will get the value and divide it through the width of the viewport minus 0.5

Then move the position of the camera while doing it
```js
window.addEventListener("mousemove", (event) => {
    mouseCoor.x = event.clientX / sizes.width - 0.5
    mouseCoor.y = -(event.clientY / sizes.height - 0.5)
    camera.position.x = mouseCoor.x
    camera.position.y = mouseCoor.y
})
```

But there is a glitch
![[chrome-capture-2022-7-23 (4).gif]]

It is because we define 2 changes on camera position, one in the y vertical scroll amd one in the y parralax, it is colliding with each other. What we could do is to group the camera so that we could update it in 2 different ways, one using the box (like the camera is inside the box) and one as the camera itself moving. 

Create a group
```js
const cameraGroup = new THREE.Group()
scene.add(cameraGroup)

cameraGroup.add(camera)
```

Update the parralax to us the camera group instead
```js
window.addEventListener("mousemove", (event) => {
    mouseCoor.x = event.clientX / sizes.width - 0.5
    mouseCoor.y = -(event.clientY / sizes.height - 0.5)
    cameraGroup.position.x = mouseCoor.x
    cameraGroup.position.y = mouseCoor.y
})
```

![[chrome-capture-2022-7-23 (5).gif]]


Next is to add some easing calculation
```js
window.addEventListener("mousemove", (event) => {
    mouseCoor.x = event.clientX / sizes.width - 0.5
    mouseCoor.y = -(event.clientY / sizes.height - 0.5)
    cameraGroup.position.x += ( mouseCoor.x - cameraGroup.position.x ) * 0.1
    cameraGroup.position.y += ( mouseCoor.y - cameraGroup.position.y ) * 0.1
})
```

This will only move the camera by 10%
![[Pasted image 20220823165454.png]]

As in the 10% of the previous 10% of the second frame. 
The problem now is that this animation easing may have different speed when it comes to high frequency. What we could do is to use a [[Delta Time]], and delta time is just the length of time from the previous frame to the now frame

```js
let prevFrame = 0 
const tick = () =>
{
    const elapsedTime = clock.getElapsedTime()
	const deltaTime = elapsedTime - prevFrame
	prevFrame = elapsedTime

    for (let meshes of meshArray) {
        meshes.rotation.x = elapsedTime * 0.1
        meshes.rotation.y = elapsedTime * 0.12
    }

    // Render
    renderer.render(scene, camera)
  
    // Call tick again on the next frame
    window.requestAnimationFrame(tick)
}
```

We need to transfer the parralax position from the eventListener to the tick function in order to apply the elapsed Time
```js
const clock = new THREE.Clock()
let prevTime = 0
const tick = () =>
{
    const elapsedTime = clock.getElapsedTime()
    const deltaTime = elapsedTime - prevTime
    prevTime = elapsedTime
  
    cameraGroup.position.x += ( mouseCoor.x - cameraGroup.position.x ) * 5 * deltaTime
    cameraGroup.position.y += ( mouseCoor.y - cameraGroup.position.y ) * 5 * deltaTime
  
    for (let meshes of meshArray) {
        meshes.rotation.x = elapsedTime * 0.1
        meshes.rotation.y = elapsedTime * 0.12
    }

    // Render
    renderer.render(scene, camera) 

    // Call tick again on the next frame
    window.requestAnimationFrame(tick)
}
```


## Particles
Add particles to enhance it
```js
const count = 300
const pointsCoor = new Float32Array(count * 3)
const pointsGeometry = new BufferGeometry()

for (let i = 0; i < pointsCoor.length; i++) {
    const i3 = i * 3
    pointsCoor[i3] = (Math.random() - 0.5) * 10
    pointsCoor[i3 + 1] = distance * 0.5 - Math.random() * distance * meshArray.length
    pointsCoor[i3 + 2] = (Math.random() - 0.5) * 10

pointsGeometry.setAttribute(
    "position",
    new THREE.BufferAttribute(pointsCoor, 3)
)

const pointsMaterial = new THREE.PointsMaterial({
    size: 0.02,
    sizeAttenuation: true
})

const pointsMesh = new THREE.Points(pointsGeometry, pointsMaterial)
scene.add(pointsMesh)
```

X is positioned randomly with a range of 10 as so as z. 
Y is positioned starting from the top then decends. This is done by dividing the distance of materials to 2 minus a random value multipled by the distance times the number of meshes.

## Scroll Trigger Animation
We could animate a mesh when it enters a viewport using manual scroll triggers, maybe also gsap [[Scroll Trigger]]?

Either way, using our previous scroll listener, ouput the value of y scroll
```js
let scrollY = window.clientY
window.addEventListener("scroll", () => {
    scrollY = window.scrollY
    camera.position.y = -scrollY / sizes.height *  distance
    console.log(scrollY)
})
```

![[Pasted image 20220824043722.png]]

The values are whole number from 0 to how many depending on the viewport size, divide it by the size of the viewport
```js
let scrollY = window.clientY
window.addEventListener("scroll", () => {
    scrollY = window.scrollY
    camera.position.y = -scrollY / sizes.height *  distance
    console.log(scrollY / sizes.height)
})
```

![[Pasted image 20220824043852.png]]

It will now output a value from 0 to 2. Round it so that when a mesh enters, a whole number pops out from 0 to 1 then assign it to a variable then prepare a storage for previous section
```js
let scrollY = window.clientY
let currentSection = 0
window.addEventListener("scroll", () => {
    scrollY = window.scrollY
    camera.position.y = -scrollY / sizes.height *  distance
    const newSection = Math.round(scrollY / sizes.height)
})
```

If the new section is not equal to the previous section, then trigger the scroll event. Use [[GSAP Programming|gsap]] to animate them and use the rotation property
```js
let scrollY = window.clientY
let currentSection = 0
window.addEventListener("scroll", () => {
    scrollY = window.scrollY
    camera.position.y = -scrollY / sizes.height *  distance
    const newSection = Math.round(scrollY / sizes.height)
    
    if (newSection != currentSection ) {
        gsap.to(meshArray[newSection].rotation, {
            x: "+=2",
            y: "+=6",
            duration: 1.5,
            ease: "power2.inOut"
        })
        currentSection = newSection
    }
})
```

The problem then is that in our tick function, we are also assigning a rotation to our meshes which then produce a glitch
```js
const clock = new THREE.Clock()
let prevTime = 0
const tick = () =>
{
    const elapsedTime = clock.getElapsedTime()
    const deltaTime = elapsedTime - prevTime
    prevTime = elapsedTime

    cameraGroup.position.x += ( mouseCoor.x - cameraGroup.position.x ) * 5 * deltaTime
    cameraGroup.position.y += ( mouseCoor.y - cameraGroup.position.y ) * 5 * deltaTime

    for (let meshes of meshArray) {
        meshes.rotation.x += deltaTime * 0.1
        meshes.rotation.y += deltaTime * 0.12
    }

    // Render
    renderer.render(scene, camera)
  
    // Call tick again on the next frame
    window.requestAnimationFrame(tick)
}
```

![[chrome-capture-2022-7-19 (223).gif]]






