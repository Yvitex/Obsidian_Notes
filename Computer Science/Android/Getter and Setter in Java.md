# Getter and Setter
This is another important part of [[OOP]] in any language
Simply creating a class in this form
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

Means you are the spawn of Satan. ![[satania-laugh.gif]]

The problem is, our attributes could be easily accessed unintentionally by others so we need to add another layer of security to prevent the code from breaking by only allowing the user to access what needs to be accessed.

To do that, we set all attributes to private
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

But what if we need the user to access it somehow? We have the key for salvation. This is by creating a getter and setter [[Java Methods]]

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

	// Example of Setter

	public void setLegs(int legs){
		this.legs = legs;
	}

	// Example of Getter

	public int getLegs(){
		return this.legs;
	}

	public void describeAnimal(){
		System.out.println("This animal have " + this.legs + " legs. It is type " + this.type + " with the name of " + this.name);
	}
}
```

Now, they can't accidentally change the values when they type
```java
object.legs = 1;
```

They need to type it as
```java
object.setLegs(1);
```




