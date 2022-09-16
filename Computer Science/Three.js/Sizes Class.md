# Size class
Next is we need te sizes class
```js
export default class Sizes{
    constructor (){
        this.width = window.innerWidth
        this.height = window.innerHeight
        this.pixelRatio = Math.min(window.devicePixelRatio, 2)

		// If resize, we will update the width and height
        window.addEventListener("resize", () => {
            this.width = window.innerWidth
            this.height = window.innerHeight
            this.pixelRatio = Math.min(window.devicePixelRatio, 2)
        })
    }
}
```

We need to trigger an event at resize, so we use the class from bruno simon called [[Event Trigger Class]]

Class size will inherit from it, we will use this trigger class 
```js
import EventEmitter from "./EventEmitter"

export default class Sizes extends EventTrigger{
    constructor (){
        this.width = window.innerWidth
        this.height = window.innerHeight
        this.pixelRatio = Math.min(window.devicePixelRatio, 2)

		// If resize, we will update the width and height
        window.addEventListener("resize", () => {
            this.width = window.innerWidth
            this.height = window.innerHeight
            this.pixelRatio = Math.min(window.devicePixelRatio, 2)
        })
    }
}
```

Use the method `trigger` to create a custom event

```js
import EventEmitter from "./EventEmitter"

export default class Sizes extends EventTrigger{
    constructor (){
        this.width = window.innerWidth
        this.height = window.innerHeight
        this.pixelRatio = Math.min(window.devicePixelRatio, 2)

        window.addEventListener("resize", () => {
            this.width = window.innerWidth
            this.height = window.innerHeight
            this.pixelRatio = Math.min(window.devicePixelRatio, 2)

			this.trigger("resize")
        })
    }
}
```

In the [[Experience Class]], instantiate this and use a trigger function called `on`
The experience method where we isntantiated resize will have the ability to detect when the `resize` is trigger. 
```js
import Sizes from "./Utils/Sizes"

export default class Experience{
    constructor (canvas) {
        this.canvas = canvas
        window.experince = this
        this.size = new Sizes()
        
        this.size.on("resize", () => {
	        console.log("trigger")
        })
    }
}
```

Separate this into a method
```js
import Sizes from "./Utils/Sizes"

export default class Experience{
    constructor (canvas) {
        this.canvas = canvas
        window.experince = this
        this.size = new Sizes()
        
        this.size.on("resize", () => {
	        this.resize()
        })
    }

	resize() {
	
	}
}
```

