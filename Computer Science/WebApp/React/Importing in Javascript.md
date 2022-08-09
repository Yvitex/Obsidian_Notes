# How Imports work in JS

## Single Export
While using [[React]], we repeatedly encounter this syntax
```js
import App from "./components/App";
```

And this syntax
```js
export default App;
```

 It actually just means to export one thing out of a code file. In fact, we could change the name of the import whatever we like because it could only just expect one thing from it.


 ## Multiple Exports
 We are not limited to only just this but we could also export multiple things at once. using `export {}`
```js
export {Pi, Euler}
```

To import this:
```js
import {Pi, Euler} from "./Component";
```

Or we could also use all, or wildcard
```js
import * as MathSymbol from "./file"
```

`MathSymbol` will become an object. So therefore...
```js
const pi = MathSymbol.Pi
const euler = MathSymbol.euler
```

```ad-Notice
collapse: open
Having both default and named exports in a single code file is acceptable. 

```

```ad-Attention
collapse: open
Import and export method is a code used in es6 though it is not very effective with 20% chance of the code not rendering to the user's browser so therefore we use, [[Babel]] to ease and convert it to become compatible with older version so in the end, we are using require() syntax... ES6? Really?
```

Related: [[Babel]]
