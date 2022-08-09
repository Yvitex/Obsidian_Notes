# This
This refers to an object. When we use this keyword in a browser, it will point to the window object
![[Pasted image 20220803040756.png]]

But with [[Reference Type]], it will points to the current object or [[Memory address]] if we use a function to do so
```js
let obj1 = {
	a: function(){
		console.log(this);
	}
}
```

![[Pasted image 20220803041209.png]]


This is an important concept when it comes to [[Javascript OOP]]
