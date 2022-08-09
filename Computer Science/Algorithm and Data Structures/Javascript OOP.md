# OOP
We could create a class using the class keyword combined with a constructor method to initialize some values.
```js
class Player{
    constructor(name, type){
		this.name = name;
		this.type = type;	
    }
    introduce(){
		console.log(`Hi, I am ${this.name} and I am a ${this.type}`)
    }
}
```

We use the [[Javascipt this keyword]] to reference the current object. 
```js
let a = new Player("Mike", "Destroyer")
a.introduce()
```

![[Pasted image 20220803042304.png]]


Another layer of this concept is [[Javascript Inheritance]]





