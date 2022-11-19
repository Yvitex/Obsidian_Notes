---
aliases: [sorting array]
---
## Documentation
Read the documentation about [Arrays](https://docs.oracle.com/en/java/javase/18/docs/api/java.base/java/util/Arrays.html)

# Java Arrays
Kinda like [[C++ Arrays]] though we create the parenthesis before setting the name of the array
```java
int[] numbers = {1, 2, 3, 4, 5};
```

Remember that arrays could only have 1 type, unlike [[Modifying List in Python|python list]]

## Predefined Arrays
They are variable arrays that is not initialized in declaration
```java
int[] numbers = new int[5];
```

In this, we need to set a fixed length. So it is not very fleximble compared to [[Javascript]] arrays ior [[Python]]'s list. If we want a more flexible [[Data Structure]], we could use [[Java ArrayList]]

Also we with this, we cannot do it like this
```java
int[] numbers = new int[5];
numbers = {1, 2, 3, 4, 5}; // wrong
```

This will only cause an error but we could assign values using [[Java Operations and Loops|for loops]] or hard coded indexes
```java
numbers[1] = 1;
numbers[2] = 2;
```

The capacity of the array can ve accessed by the length
```java
System.out.println(numbers.length);
```

This will output 5. But notice that the  length is only 2. Length and capacity is different.

## Sorting array
We could sort unsorted arrays in java simply by calling the Arrays module
```java
import java.util.Arrays;

int[] numbers = {2, 5, 1, 4};
```

Use the builtin sort method
```java
int[] numbers = {2, 5, 1, 4};
Arrays.sort(numbers);
```

Remember that this sort method is a [[Java Methods|void method]], therefore it does not return a value but affects the original array.
```java
int[] numbers = {2, 5, 1, 4};
Arrays.sort(numbers);
System.out.println(numbers);
```