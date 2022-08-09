# Overloading Constructor
Another [[OOP]] concept for [[JAVA]]

Java does not support default parameter like [[Python]] but... they could create any number of [[Java Constructor]] increasing the flexibility of the classes. This is called *overloading constructor*

```java
public Animal{
	private int legs;
	private String name;
	private String type;

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

If we have this, we could add another constructor using the same name
```java
public Animal{
	private int legs;
	private String name;
	private String type;

	public Animal(int legs, String name, String type){
		this.legs = legs;
		this.name = name;
		this.type = type;
	}

	public Animal(){}

	public void describeAnimal(){
		System.out.println("This animal have " + this.legs + " legs. It is type " + this.type + " with the name of " + this.name);
	}
}
```

We just created a constructor that the code will use when in our main method, we use the class without declaring any parameters. 

We could add another one that will handle if we have additional data
```java
public Animal{
	private int legs;
	private String name;
	private String type;

	public Animal(int legs, String name, String type){
		this.legs = legs;
		this.name = name;
		this.type = type;
	}

	public Animal(){}

	public Animal(int legs, String name, String type, String breed){
		this.legs = legs;
		this.name = name;
		this.type = type;
		this.breed = breed;
	}

	public void describeAnimal(){
		System.out.println("This animal have " + this.legs + " legs. It is type " + this.type + " with the name of " + this.name);
	}
}
```
