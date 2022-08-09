# Java Constructor
To make our lives more easier, we could set up the [[JAVA OOP Atttributes|initial data]] required to our classes, we could make a constructor to aid us
```java
public class Shape{
	int length;
	int width;
	String color;
	String shape;

	public Shape(){
	
	}
}
```

`public Shape()` is a constructor, we could not set parameters to be required.
```java
public class Shape{
	int length;
	int width;
	String color;
	String shape;

	public Shape(int length, int width, String color, String shape){

	}
}
```

For every parameters we setup, we set it to a [[Java OOP Methods|this keyword]] variable that is already setup above
```java
public class Shape{
	int length;
	int width;
	String color;
	String shape;

	public Shape(int length, int width, String color, String shape){
		this.length = length;
		this.width = width;
		this.color = color;
		this.shape = shape;
	}
}
```

Now in our main method, the setup would now become
```java
public class Main{
	public static void main(String[] args){
		Shape shape = new Shape(2, 1, "blue", "rectangle");
	}
}
```

