# How to create our own geometry?
As `Three.Geometry` constructor is now depreceted, we don't have a choice but to use `Three.BufferGeometry()`

## Storing Buffer Geometry Data
Buffer geometry could only store a float.
data points must be
- An array
- A float
- Fixed Size
- Easier for the computer to handle

## How to
1 face == 1 triangle.  To create a single triangle, we first set up our `BufferGeometry()` instance
```js
const geometry = new THREE.BufferGeometry();
```

Next is we create the coordinates of each point location, because Buffer only acceots float in arraym we use `Float32Array`
```js
const geometry = new THREE.BufferGeometry();
const positions = new Float32Array([0, 0, 0, 0, 1, 0, 1, 0, 0]); 
```

We will divide this by 3, where for each group must have 3 datas. Meaning our coordinates are (0, 0, 0) = origin, (0, 1, 0) move one step at y axis, (1, 0, 0) move one step at x axis, To set this to an attribute, we insert this as a parameter in `THREE.BUfferAttribute()`
```js
const geometry = new THREE.BufferGeometry();
const positions = new Float32Array([0, 0, 0, 0, 1, 0, 1, 0, 0]); 
const bufferAttributes = new THREE.BufferAttributes(position, 3);
```

We set the second param as 3 because we are separating each 3 values to each other. Next is to integrate this with the geometry object
```js
const geometry = new THREE.BufferGeometry();
const positions = new Float32Array([0, 0, 0, 0, 1, 0, 1, 0, 0]); 
const bufferAttributes = new THREE.BufferAttributes(position, 3);
geometry.setAttribute('position', bufferAttributes);
```

![[Pasted image 20220706151604.png]]

To create multiple lumps of trinagles, we create a for loop
```js
const count = 50; // amount of triangle
const positions = new Float32Array(count * 3 * 3)

for(let i = 0; i < count * 3 * 3; i++){
	positions[i] = Math.random();
}
```

Now we set the length of array as count * 3 * 3 as each triangle have 3 vartices, each [[Three.js Geometry|vertices]] contains 3 values. Then we set each empty element with a random value. 

```js
const count = 50; // amount of triangle
const positions = new Float32Array(count * 3 * 3)

for(let i = 0; i < count * 3 * 3; i++){
	positions[i] = Math.random();
}

const bufferAttr = new THREE.BufferAttribute(positions, 3);
const geometry = new THREE.BufferGeometry();
geometry.setAttribute('position', bufferAttr);
```

Here. we set the attributes to the geometry object.![[chrome-capture-2022-6-6(7).gif]]
