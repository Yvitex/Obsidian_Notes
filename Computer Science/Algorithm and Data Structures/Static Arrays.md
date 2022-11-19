# Static Arrays
In static typed programming language, arrays need a size number that will define the number of items stored to one array. Why? Because we don't want it to take too much space that what is needed

It requires to specify space for the arrays. The length is fixed and can't be changed lke in [[Java Arrays]]

```java
int[] numbers = new int[5];
```

In static arrays, we have 2 kinds of length, the capacity and the length of arrays. Capacity is the total number of item that the array could hold while the length is the number of item inside the array. 

The example above have a capacity of 5 but a length of 0 as we haven't yet inserted items inside it,

In [[Java Arrays]], we could call the capacity by using `.length` property and the length, well, using a loop or something else. But in a problem, if the arrays are given as a parameter, it is safe to assume that length == capacity. 


