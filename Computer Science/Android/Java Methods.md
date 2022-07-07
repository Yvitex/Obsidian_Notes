# Java Methods

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

It is so similar to [[Python Programming]]'s, functions but more wordy. 
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

