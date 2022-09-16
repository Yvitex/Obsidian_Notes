# Camera Class
Instantiate the [[Three.js (core)]] in the [[Experience Class]]
```js
import Camera from "./Utils/Camera"
import Sizes from "./Utils/Sizes"
import Time from "./Utils/Time"
import * as THREE from "three"

export default class Experience{
    constructor (canvas) {
        this.canvas = canvas
        window.experience = this
        this.size = new Sizes()
        this.time = new Time()
        this.camera = new Camera()
        this.scene = new THREE.Scene()

        this.size.on("resize", () => {
            this.resize()
        })
  
        this.time.on("tick", () => {
            this.update()
        })
    }

    resize() {
    }
    
    update() {
    }
}
```

Create the camera class
```js
export default class Camera{
    constructor() {

    }
}
```

## Getting the Experience Details
First Solution.
Now, what we need with the [[Three.js Camera|camera]] is to have access with the [[HTML Canvas]] and the [[Sizes Class]], 
we could all have that by accessing the [[Experience Class]]. We have 3 ways of doing this. remember this code above
```js
window.experience = this
```

We could do it like this
```js
export default class Camera{
    constructor() {
        this.experience = window.experience
        console.log(this.experience.size.width) // access to te size width
    }
}
```

The problem is that, global variable are messy creatures

Second solution.
Pass the class as a parameter like this
```js
this.camera = new Camera(this)
```

Then use it like a normal parameter in the class code
```js
export default class Camera{
    constructor(experience) {
        this.experience = experience
        console.log(this.experience.size.width) // access to width
    }
}
```

Third solution is the most complicated
We coudl just pass it as an instance but first we need to only pass it as a [[Singleton]] meaning no matter how many times we instantiated, we will not create a new object but the same thing from the first instance
The conde in the [[Experience Class]] is like this
```js
import Camera from "./Utils/Camera"
import Sizes from "./Utils/Sizes"
import Time from "./Utils/Time"
import * as THREE from "three"

let instance = null // create a container that will check if it is instantiated or not
export default class Experience{
    constructor (canvas) {

        if (instance) { // if the instance is not null, we return the instance and cut the program
            return instance
        }
        
        instance = this // f  the instance is null, then we proceed to create a new object
        this.canvas = canvas
        window.experience = this
        this.size = new Sizes()
        this.time = new Time()
        this.camera = new Camera()
        this.scene = new THREE.Scene()
  
        this.size.on("resize", () => {
            this.resize()
        })

        this.time.on("tick", () => {
            this.update()
        })
    }
```

In the camera  class, we do it liek this
```js
import Experience from "../Experience";
export default class Camera{
    constructor() {
	    this.experience = new Experience()
        console.log(this.experience.size.width)
    }
}
```


## Creating Camera
Using the third solution, we could prepare the detail property of our class such as the width and height of the viewport, the [[HTML Canvas]], and the [[Three.js Scene|scene]]
```js
import Experience from "../Experience";
export default class Camera{
    constructor() {
	    this.experience = new Experience()
		this.size = this.experience.size
        this.canvas = this.experience.canvas
        this.scene = this.experience.scene
    }
}
```

Create a method tha will create the [[Three.js Camera|camera]]
```js
setInstance() {
	this.instance = new PerspectiveCamera(35, this.size.width/this.size.height, 0.1, 100)
	this.instance.position.set(6, 4, 8)
	this.scene.add(this.instance)
}
```

Create the [[Orbit Controls]] for te camera
```js
setOrbitControl() {
	this.control = new OrbitControl(this.instance, this.canvas)
	this.control.enabledDamping = true
}
```

Create a resize method that will triger on resize
```js
resize() {
	this.instance.aspect = this.size.width / this.size.height
	this.instance.updateProjectionMatrix()
}
```

Create an update method for controls
```js
update() {
	this.control.update()
}
```

Set the orbit control method and instance at the constructor
```js
import Experience from "../Experience";
export default class Camera{
    constructor() {
	    this.experience = new Experience()
		this.size = this.experience.size
        this.canvas = this.experience.canvas
        this.scene = this.experience.scene
	    this.setInstance()
		this.setOrbitControl()
    }
}
```

Resize and update will trigger on the [[Experience Class]]
```js
export default class Experience{
    constructor (canvas) {

        if (instance) { // if the instance is not null, we return the instance and cut the program
            return instance
        }
        
        instance = this // f  the instance is null, then we proceed to create a new object
        this.canvas = canvas
        window.experience = this
        this.size = new Sizes()
        this.time = new Time()
        this.camera = new Camera()
        this.scene = new THREE.Scene()
  
        this.size.on("resize", () => {
            this.resize()
        })

        this.time.on("tick", () => {
            this.update()
        })

		resize() {
			this.camera.resize()
		}

		update() {
			this.camera.update()
		}
    }
```

Orbit controll will update for every execution of tick function. Resize will occur for every trigger in resize.




