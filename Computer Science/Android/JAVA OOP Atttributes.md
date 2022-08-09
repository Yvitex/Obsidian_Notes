# Java OOP
[[OOP]] style [[JAVA]] code. 

## Simple
Lets say you have a main method
```java
class Main{
	public static void main(String[] args){
		
	}
}	
```

We could create a new class in another file
```java
class Motorcycle{
	float version;
	String brand;
	String plateNumber;
}
```

To assign value from the main method, we instantiate the class fist by using keyword `new`. Also the variable type is customized
```java
class Main{
	public static void main(String[] args){
		Motorcycle suzuki = new Motorcycle();
	}
}	
```

Next is to assignt he values using the dot method
```java
class Main{
	public static void main(String[] args){
		Motorcycle suzuki = new Motorcycle();

		suzuki.version = 2.2f;
	}
}	
```

We could create any number of isntances
```java
class Main{
	public static void main(String[] args){
		Motorcycle suzuki = new Motorcycle();
		Motorcycle kawazaki = new Motorcycle();

		suzuki.version = 2.2f;
		kawazaki.version = 1.2f;

		System.out.println(suzuki.version);
		System.out.println(kawazaki.version);
	}
}
```

Remember that in [[Java Variables]], float must have a prefix of f each value.
![[Pasted image 20220710052247.png]]


Now, how can create [[Java OOP Methods]], we could also implify setting those attribute using a [[Java Constructor]]
