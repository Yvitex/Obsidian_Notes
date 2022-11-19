# Array DataStructure Code
Here we are using [[Javascript]] syntax but we could do it in any kind of language
```js
class myArray{
	constructor(...elements){
		this.arrays = {...elements} // spread operation
		this.length = elements.length
	}
}
```

`this.arrays` will be an object, each have its own automatically labeled indexes. And yes, arrays is just an object indeed, 
This will initialize the array and that's it. We could ccall it like this
```js
let newArray = new myArray(1, 2, 3, 4, 5);
console.log(newArray)
```

![[Pasted image 20220803055031.png]]

The get method by index works like this applied inside the class
```js
get(index) {
	const element = this.arrays[index];
	console.log(element);
	return element
}
```

We are simply getting the element in the specific key of the object array.
```js
data.get(4)
```

Output: 5

The push method is simply applying a new value in  the last index which is the same as its length.
```js
push(element) {
    this.arrays[this.length] = element;
    this.length++;
    return this.length
}
```

Will return the length which is incremented as we apply more and more elements. 
Pop method is just removing the last index and decrementing the length by 1.
```js
pop() {
    const element = this.arrays[this.length];
    this.length--;
    delete this.arrays[this.length];
    return element;
  }
```

The delete method needs to loop fro the specified index to the current. Here we need 2 functions, one function is responsivle in looping through the array to move the elements in the previous indexes therefore making it an [[Linear  Time Complexity|O(n)]], It also needs to delete the last element that will be a duplicate. 
```js
delete(index) {
	this.length--;
    this.shiftdown(index)
}

shiftdown(index) {
	for (let i = index; i < this.length; i++) {
	    this.arrays[i] = this.arrays[i + 1]
    }
    delete this.arrays[this.length]
}
```

Actually, we could compress it into one.
```js
delete(index) {
	for (let i = index; i < this.length; i++) {
      this.arrays[i] = this.arrays[i + 1]
    }
    
    this.length--;
    delete this.arrays[this.length]
  }
```


