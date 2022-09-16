# Time Class
```js
import EventEmitter from "./EventEmitter";

export default class  extends EventEmitter{
    constructor() {
        super()
        this.start = Date.now()
        this.delta = 16 // temporary value
        this.current = this.time
        this.elapsed = 0

        window.requestAnimationFrame(() => {
            this.tick()
        })
    }

    tick() {
        this.dateNow = Date.now()
        this.delta = this.dateNow - this.current
        this.current = this.dateNow
        this.elapsed = this.start - this.current
        this.trigger("tick")
        window.requestAnimationFrame(() => {
            this.tick()
        })
    }
}
```

