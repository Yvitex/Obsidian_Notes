# Inheritance
An important concept in [[Javascript OOP]].

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

We could create this by using the extends keyword and super constructor
```js
class Samurai extends Player{
    constructor(name, type){
      super(name, type);
    }
    selfDestruct(){
      console.log(`${this.name} the ${this.type} died unexpectedly`)
    }
}
```

Now we could call both introduce() and selfDestruct() if we instatiate it using the samurai class
```js
let b = new Samurai("Retri", "Unsheated")
b.introduce()
b.selfDestruct()
```

![[Pasted image 20220803043021.png]]

