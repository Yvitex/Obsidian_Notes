---
aliases: [method overriding, super keyword, superclass]
---
# Java Inheritance
Anothe [[OOP]] priciple. But there is a little twist when it comes to [[JAVA]] programming

The main method boilder plate
```java
public class Yeah {
	public static void main(String[] args) {	
	}
}
```

We have a class called animal with some default parameters
```java
public Animal{
	int legs;
	String name;
	String type;

	public Animal(int legs, String name, String type){
		this.legs = legs;
		this.name = name;
		this.type = type;
	}

	public void describeAnimal(){
		System.out.println("This animal have " + this.legs + " legs. It is type " + this.type + " with the name of " + this.name);
	}
}
```

We could create another class that will inherit the [[Java OOP Methods|methods]]  and [[JAVA OOP Atttributes|attributes]],
We simply add the keyword `extends` then the name of the class we are trying to get
```java
public Breed extends Animal{
	
}
```

We could add a unique attribute and method for it or else it will be useless to create it
```java
public Breed extends Animal{
	String breed;

	public void describeBreed(){
		System.out.println("The breed is called " + this.breed)
	}
}
```

Now we could call this class to the main method and call this method, even the method existing in the animal class and even we could set up the variables from the Animal class, for example
```java
public class Yeah {
	public static void main(String[] args) {	

		Breed askal = new Breed();
		askal.legs = 4;
		askal.name = "Doggy";
		askal.type = "Mammal";

		askal.describeAnimal();
		
	}
}
```
![[Pasted image 20220710111620.png]]

Or even call its own method.
```java
public class Yeah {
	public static void main(String[] args) {	

		Breed askal = new Breed();
		askal.legs = 4;
		askal.name = "Doggy";
		askal.type = "Mammal";
		askal.breed = "Askal";

		askal.describeBreed();
		
	}
}
```
![[Pasted image 20220710111758.png]]

```ad-Danger
title: It will inherit attribute and methods
collapse: open
Yes it will inherit the attributes and methods of the parent class but not the [[Java Contructor|constructor]].

```

So what we must do to inherit the [[Java Constructor]] is to create a super constructor.
```java
public Breed extends Animal{
	String breed;

	public Breed(int legs, String name, String type, String breed){
		super(legs, name, type);
		this.breed = breed;
	}

	public void describeBreed(){
		System.out.println("The breed is called " + this.breed)
	}
}
```

## Overriding
This will basically override the parent method.
```java
public Breed extends Animal{
	String breed;

	public String describeBreed(){
		return "The breed is called " + this.breed;
	}

	@Override
	public String describeAnimal(){
		return super.describeAnimal() + ". " + describeBreed();
	}
}
```

Super method will execute the original method that will return the oiginal string from Animal class.
```ad-Attention
collapse: open
Remember, we can't concatenate void method with a return method so I replaced every method with a return value
```

```java
public Animal{
	int legs;
	String name;
	String type;

	public Animal(int legs, String name, String type){
		this.legs = legs;
		this.name = name;
		this.type = type;
	}

	public String describeAnimal(){
		return "This animal have " + this.legs + " legs. It is type " + this.type + " with the name of " + this.name;
	}
}
```

We could also override from the superclass object called Object. One of itsmethod is `toString()`. When we print out the name of an object such as
```java
public class Yeah {
	public static void main(String[] args) {	

		Breed askal = new Breed(4, "Doggy", "Mammal", "Askal");
		System.out.println(askal);
		
	}
}
```

This will just output some [[Memory address]]. In the background, it is calling the `toString()` method so if we override it like
```java
public Breed extends Animal{
	String breed;

	public String describeBreed(){
		return "The breed is called " + this.breed;
	}

	@Override
	public String describeAnimal(){
		return super.describeAnimal() + ". " + describeBreed();
	}

	@Override
	public String toString() {
		return "Breed class information: " + this.breed + "\nMemory Address: " + super.toString();
	}
}
```

When we print it again
```java
public class Yeah {
	public static void main(String[] args) {	

		Breed askal = new Breed(4, "Doggy", "Mammal", "Askal");
		System.out.println(askal);
	}
}
```
![[Pasted image 20220710164039.png]]

## Superclass Object
![[Pasted image 20220710143754.png]]

All classes and even [[Java Variables|strings]] inherits from the almighty superclass called Object. Then we create another class that inherits from the animal class. The deeper the heirarchy, the more specific it become, while the parent class contains the general ones. This keeps us  saving a lot of memory in the program. 