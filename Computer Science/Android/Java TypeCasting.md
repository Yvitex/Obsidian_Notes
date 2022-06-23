# Java Operation and Type Casting
Integer could only accept an integer, a float would only accept a float just like how beautiful women only accepts handsome men and how rich men only accepts rich women, except when they have the beauty, bruh. 

## Example
```
float num1 = 1f;
float num2 = 2f;

int answer = num1 + num2;
```

Will output an error, to make this appropriate, then we use *type casting* where we transform the float into an itneger
```
float num1 = 1f;
float num2 = 2f;

int answer = (int) (num1 + num2);
```

Also, when printing numbers, be carefully in using the [[Java Operations and Loops|operation]] '+' that concatenates string, example
```
int a = 2; 
int b = 2;

System.out.println("The answer is " + a + b);
```

Will output: The answer is 22.

What we should do is to specify that we want to mathematically add it rather than to concatenate it like a [[Java Variables|string]]
```
System.out.println("The answer is " + (a + b));
```

Will output: The answer is 4.