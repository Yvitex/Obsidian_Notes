# Javascript
## Math Function
### Random Number
```js
var number = Math.random() * 10;
```

### Round Number
```js
var number = Math.round(32.21)
```

## Date and Time Module
### Date Module
```js
const time = new Date();
```

### Get time in String
```js
const time = new Date().getLocaleTimeString("en-US", {h12: false});
```

### Execute Function Repeatedly
```js
function sayHi(){
	console.log("Say Hi");
}
setInterval(sayHi, 1000); //execite per 1 second
```

### Date now
[[UNIX Time]] Scale Date 
```js
let time = Date.now();
```

## Event Listener
### Mousemove
```js
window.addEventListener('mousemove', (event) =>{
	console.log("x: " + event.clientX + " y:" + "event.clientY");
})
```

See the documentation [here](https://www.w3schools.com/jsref/jsref_obj_date.asp)
