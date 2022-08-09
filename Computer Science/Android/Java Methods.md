---
aliases: [void method]
---
# Java [[OOP|Methods]]

## Void Method
Void methods are methods that do not return a value. 
One example of a method is the most common `main` method
```
public static void main(String[] args){

}
```

This method executes automatically which is why it is the main, or the center of the code. Without it, the code won't run, but we could also make our own method just like so such as

```
public static void sayHello(){
	System.out.println("Hello World");
}
```

This method won't execute unless we call it inside main method so
```
public static void main(String[] args){
	sayHello();
}
```

It is so similar to [[Python]]'s, functions but more wordy. 
![[Pasted image 20220617163416.png]]

`void` specifies if we have a return value or nah

### With Parameters
We need to specify the data type of the parameters, for example
```java
public static void sayHello(String name){
	System.out.println("Hello World and " + name);
}
```

Inside the main method, we do,
```
public static void main(String[] args){
	sayHello("Aliana");
}
```

![[Pasted image 20220617154703.png]]

## Passing Array
We could also pass an array to a method with the propert syntax
```java
public static void summationArrays(int[] numbers){
	int i;
	int summation = 0;
	for(i = 0; i < numbers.length; i++){
		summation += numbers[i];
	}
}
```

## Passing Objects
If we could pass arrays, we could also pass objects using this syntax, `Animal` is the class. 
```java
public void addLegs(Animal animal){
	animal.setLegs(animal.getLegs + 1);
}
```

The rest of the code is
```java
public class MagicalGurl {
	String name;
	String magicType;
	
	public MagicalGurl(String name, String magicType) {
		this.name = name;
		this.magicType = magicType;
	}
	
	public void addLegs(Animal animal) {
		animal.setLegs(animal.getLegs() + 1);
	}
}
```

The code is inside the MagicalGurl class and Animal class with this code with [[Getter and Setter in Java]] and [[Java Constructor]]
```java
public class Animal{
	
	private int legs;
	private String name;
	private String type;
	
	public Animal(int legs, String name, String type) {
		this.legs = legs;
		this.name = name;
		this.type = type;
	}
	
	public void setLegs(int legs) {
		this.legs = legs;
	}
	
	public int getLegs() {
		return this.legs;
	}
	
	public String describeAnimal() {
		return "This animal have " + this.legs + " legs. It is type " + this.type + " with the name of " + this.name;
	}
	
}
```

To call it inside hte main method
```java
public class Main{
	public static void main(String[] args){
		Animal animal = new Animal(4, "Ere", "Shitzu");
		MagicalGurl magician = new MagicalGurl("Mika", "Mendelian Genetics");

		magician.addLegs(animal);
		System.out.println(animal.getLegs());
	}
}
```

Will output 5

## With Return Values

We simply replace `void` with a data [[Java Variables|data type]] 
```
public static String sayHello(String name){
	return "Hello World and " + name;
}
```

Inside the main methodm because we are return a value that can be catched by a [[Java Variables]], we could print it out to output the value
```
public static void main(String[] args){
	System.out.println(sayHello("Aliana"));
}
```

