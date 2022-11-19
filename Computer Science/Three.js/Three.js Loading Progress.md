---
aliases: []
---
# Three.js Loading Progress
We could create a loading progress in [[Three.js (core)]] by overlaying a plane over the camera during the intro of the [[Three.js Scene|scene]]. We must be interested to do it as some [[Three.js Mesh|mesh]] don't load right after you open the application but rather loads while you are seeing the scene. What we want is to see everything necessary as we loaded the scene and not right after.

Instead of creating a new div element in [[HTML]], and design it using [[CSS]], we could just create a new [[Shader]] that will do this for us. So first, create a new Plane [[Three.js Mesh|mesh]] and add it to the scene

```js
const overlayGeometry = new THREE.PlaneBufferGeometry(1, 1, 1, 1)
const overlayMaterial = new THREE.MeshBasicMaterial()
const overlay = new THREE.Mesh(overlayGeometry, overlayMaterial)
scene.add(overlay)
```

To do what we want,  we use the [[Create Shaders in Three.js|ShaderMaterial()]]. Write the boiler plate
```js
const overlayGeometry = new THREE.PlaneBufferGeometry(1, 1, 1, 1)
const overlayMaterial = new THREE.ShaderMaterial({
    vertexShader: `
        void main(){
            gl_Position = projectionMatrix * modelViewMatrix * vec4(position, 1.0);
        }
    `,
    fragmentShader: `
        void main(){
            gl_FragColor = vec4(1.0, 0.0, 0.0, 1.0);
        }
    `
})

const overlay = new THREE.Mesh(overlayGeometry, overlayMaterial)
scene.add(overlay)
```

![[Pasted image 20220915032709.png]]

We could see the plane exist. What we could do stop its rotation is to remove the `projectionMatrix` and `modelViewMatrix` 
```js
const overlayMaterial = new THREE.ShaderMaterial({
    vertexShader: `
        void main(){
	        // Remove the matrices
            gl_Position = vec4(position, 1.0); 
        }
    `,
    fragmentShader: `
        void main(){
            gl_FragColor = vec4(1.0, 0.0, 0.0, 1.0);
        }
    `
})

```

![[Pasted image 20220915032900.png]]

Now it is overlayed. Expand the plane to fit it by increasing simply its width and height
```js
const overlayGeometry = new THREE.PlaneBufferGeometry(1, 1, 1, 1)
```

![[Pasted image 20220915033058.png]]

Now it is filled with reds. Turn it to black by simply modifying the [[Fragment Shader GLSL]], also, we need to modify the opacity. It will first in the form of solid black and later on, when all [[Three.js Textures]] and models are loaded, we'll make it transparent and disappear. Here, we'll use a [[Shader Uniform]]
```js
const overlayMaterial = new THREE.ShaderMaterial({
	transparent: true,
	uniforms: {
		uAlpha: {value: 0.5}
	},
    vertexShader: `
        void main(){
	        // Remove the matrices
            gl_Position = vec4(position, 1.0); 
        }
    `,
    fragmentShader: `
	    uniform float uAlpha;
        void main(){
            gl_FragColor = vec4(1.0, 0.0, 0.0, uAlpha);
        }
    `
})
```

![[Pasted image 20220915034803.png]]

Now we'll animate the opacity using [[GSAP Programming|gsap]]
First we need to create a [[Three.js Loading Manager]], we only have one model in the scene composed of several models imported using [[GLTFLoader()]]
```js
const loadingManager = new THREE.LoadingManager(
    // Loaded
    () => {
        console.log("loaded");
    },
    // Progress
    () => {
        console.log("progress")
    }
)

const gltfLoader = new GLTFLoader(loadingManager)
```

![[Pasted image 20220915040200.png]]

It is working at least. Now import the [[GSAP Programming|gsap]] and then use it in the loaded callback to reduce the opacity of the [[Shader]] material who's opacity is on 1 by default. Use the [[gsap.to()]] method
```js
const loadingManager = new THREE.LoadingManager(
    // Loaded
    () => {
	    // animation
        gsap.to(overlayMaterial.uniforms.uAlpha, {value: 0, duration:3})
    },
    // Progress
    () => {
        console.log("progress")
    }
)
```

![[chrome-capture-2022-8-15.gif]]

We could add some loading bar. But first, we need to do some [[Network Throttling]] to slower thid down. 
Add a div element in the [[HTML]]
```html
<body>
    <canvas class="webgl"></canvas>
    <div class="loader"></div>
</body>
```

Class `loader` will have to this styling so that it would look like a loading bar
```css
.loader{
    position: absolute;
    top: 50%;
    width: 100%;
    height: 2px;
    background-color: white;
}
```
![[Pasted image 20220915044255.png]]

We could animate it using `transform` property
```css
.loader{
    position: absolute;
    top: 50%;
    width: 100%;
    height: 2px;
    background-color: white;
    transform: scaleX(0.3);
}
```

![[Pasted image 20220915044538.png]]

We want the transformation to start from the left, therefore we must change the origin from the default `center` to `top left`
```css
.loader{
    position: absolute;
    top: 50%;
    width: 100%;
    height: 2px;
    background-color: white;
    transform: scaleX(0.3);
    transform-origin: top left;
}
```

We could animate it inside [[Javascript]] using the [[DOM]]
```js
const progressBar = document.querySelector(".loader")
```

Inside the progress callback at the [[Three.js Loading Manager]], we could call 3 arguments and they are the url, the amount of object loaded, and the total items to load, we could calculate the progress by simple dividing the loaded over the items to load. We could access the style using the `style` then `transform` property.
```js
const loadingManager = new THREE.LoadingManager(
    // Loaded
    () => {
	    // animation
        gsap.to(overlayMaterial.uniforms.uAlpha, {value: 0, duration:3})
    },
    // Progress
    () => {
        const loadedRatio = itemsLoaded / itemsToLoad
        progressBar.style.transform = `scaleX(${loadedRatio})`
    }
)
```

We then try to smoothen the animation using the `transition` property in css
```css
.loader{
    position: absolute;
    top: 50%;
    width: 100%;
    height: 2px;
    background-color: white;
    transform: scaleX(0.3);
    transform-origin: top left;
    transition: transform 0.5s;
}
```

![[chrome-capture-2022-8-15 (1).gif]]

Now we could remove this thing using another class animation

```css
.loader.ended{
	transform: scaleX(0);
    transform-origin: top right;
    transition: transform 1.5s ease-in-out;
}
```

This will simply change the origin to the right then shrink it out with some easing function. We add this using [[Javascript]] 
```js
const loadingManager = new THREE.LoadingManager(
    // Loaded
    () => {
        gsap.to(overlayMaterial.uniforms.uAlpha, {value: 0, duration:3})
        // Finished loading aniamtion
        progressBar.classList.add("ended")
        progressBar.style.transform = ``
    },
    // Progress
    (url, itemsLoaded, itemsToLoad) => {
        console.log("progress")
        const loadedRatio = itemsLoaded / itemsToLoad
        progressBar.style.transform = `scaleX(${loadedRatio})`
    }
)
```

We also override the previous javascript code in styling so that it won't hinder our scale in [[CSS]]
We may want to put this into a delay or a [[Javascript]] timeout function with 500 ms delay
```js
() => {
	window.setTimeout(() => {
		gsap.to(overlayMaterial.uniforms.uAlpha, {value: 0, duration:3})
		progressBar.classList.add("ended")
		progressBar.style.transform = ``
	}, 500)
},
```

![[chrome-capture-2022-8-15 (2).gif]]

# Metatags
###### Related: 
[[Three.js (core)]], [[GSAP Programming|gsap]], [[CSS]]
###### Tags:
#three #web-animation #javascript 

---