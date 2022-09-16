# Experience class
Create the experience Js. The basic code is like this
```js
import Sizes from "./Utils/Sizes"

export default class Experience{
    constructor (canvas) {
        this.canvas = canvas
        window.experince = this
        this.size = new Sizes() // Will be added later
    }
}
```