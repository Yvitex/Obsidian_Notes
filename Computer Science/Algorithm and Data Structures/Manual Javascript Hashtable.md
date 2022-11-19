# Hashtable
To construct a [[Hash Table]], we could utilize the power of [[Array Data Structure]]

```js
class HashTable(){
	constructor(length){
		this.data = new Array(length);
	}
}
```

One of its method is a [[Hashing Function]] that converts text into numerical data that specifies in what [[Memory address]] would the data go depending on the key
```js
_hash(string){
	let hash = 0;
	for (let i = 0; i < string.length; i++) {
		hash = (hash + string.charCodeAt(i) * i) % this.data.length;
	}
	return hash;
}
```

We modulo it to the length to limit it to the total array length of memory space
The set keyword is a function that accepts key and value pair that adds an array of value inside each array and if something already else exist, then we will push it also to the same array making a multidimensional array
```js
set(key, value) {
	let hash_val = _hash(key);
	if (this.data[hash_val] == null) {
		this.data[hash_val] = [];
	}
	this.data[hash_val].push([key, value]);
	return this.data;
}
```

The [[Algorithm]] used is that when the array item in the specified hash is empty, then we will add an empty array in order to enable us to push a key value pair in that array. 

Get on the other hand accepts one parameter called key, we will also hash it and using the hash [[Memory address]], we will output the value of that key.

```js
get(key) {
	let hash_val = _hash(key);
	if (this.data[hash_val].length > 1) {
		for(let i = 0; i < this.data[hash_val.length], i++) {
			if (this.data[hash_val][i][0] == key) {
				console.log(this.data[hash_val][i][1])
			}
		}
	}

	else {
		console.log(this.data[hash_val][0][1])
	}
}
```

HEre we will be implementing the `keys()` method. This method will traverse the array to collect the keys
```js
key() {
	const keyArrays = [];

	for (let i = 0; i < this.data.length; i++) {
		if (this.data[i] && this.data[i].length > 1) {
			for (let j = 0; j < this.data[i].length; j++) {
				keyArrays.push(this.data[i][j][0]);
			}
		}

		else if (this.data[i] && this.data[i].length == 1) {
			keyArrays.push(this.data[i][0][0]);
		}

	}
	
	return keyArrays;
}
```


As we could see, this method is a [[Quadratic Time|O(n^2)]] as we are creating a nested for loop. 