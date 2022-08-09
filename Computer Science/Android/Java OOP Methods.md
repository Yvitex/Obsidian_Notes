---
aliases: [static method, this keyword]
---
# Java OOP Methods
[[JAVA]] for [[OOP]]. 

## Non Static method
We could create it by simply creating a simple function. THough we must decide if it is static or not. 
```java
public class Shape {
	int length;
	int width;
	String color;
	String shape;
	
	public String describe() {
		return "Description: \nShape: " + this.shape + "\nColor: " + this.color + "\nArea: " + this.length * this.width;
	}
}
```

A nons static method simply means it is a method available for the instance of the class but a static method is a method that is only used inside the class. 

Also regarding the use of *this*, we always use it inside a class to reference the current object we are in. We cannot use this keyword when we are working with static methods which require us to state the variable to be used  as static. 

To call this method in the main method
```js
public class Yeah {

	public static void main(String[] args) {
		Shape shape = new Shape();
		
		shape.shape = "Rectangle";
		shape.color = "red";
		shape.length = 2;
		shape.width = 1;
		
		System.out.println(shape.describe());
		
	}
}
```
![[Pasted image 20220710055817.png]]
