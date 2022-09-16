# Debug Class
Import the dat gui
```js
import * as dat from "lil-gui"
```

Create a constructor
```js
export default class Debug{
    constructor() {

        }
    }
}
```

Create a hash that we could access through a link like this
![[Pasted image 20220830151609.png]]

Is to access the `window.location.hash`, when we type a string next to #, it will be considered a hash and that property will  ouput it so what we could do is to test if it is equals to `#debug`
```js
this.active = window.location.hash == "#debug"
```

If that is true, we will create an instance of debugger
```js
export default class Debug{
    constructor() {
        this.active = window.location.hash == "#debug"

        if(this.active) {
            this.ui = new dat.GUI()
        }
    }
}
```

To make this functional, for example, go to the [[Model or Fox Class]] and do some animation using it. 

First, if the debugger is active. create a folder.
```js
if (this.debug.active) {
    this.foxDebug = this.debug.ui.addFolder("Fox")
}
```

Now in the animation, create some individual actions of animation, and create a function that will smooth the transition between one action to another
```js
setAnimation() {
	this.animation = {}
	this.animation.mixer = new THREE.AnimationMixer(this.model)
	this.animation.action = {}

	// Individual Actions
	this.animation.action.idle = this.animation.mixer.clipAction(this.resource.animations[0])
	this.animation.action.walking = this.animation.mixer.clipAction(this.resource.animations[1])
	this.animation.action.running = this.animation.mixer.clipAction(this.resource.animations[2])

	// Initial play action
	this.animation.action.current = this.animation.action.idle
	this.animation.action.current.play()

	// Function tat will smooth the transition
	this.animation.play = (name) => {
		const newAction = this.animation.action[name]
		const oldAction = this.animation.action.current

		// Reset first then play
		newAction.reset()
		newAction.play()

		// Crossfade will the one that will smooth the animation
		newAction.crossFadeFrom(oldAction, 1)
		this.animation.action.current = newAction
	}
```

In the environment, we could do the same

![[Pasted image 20220830152554.png]]

