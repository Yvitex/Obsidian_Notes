# Java Operations
## Mathematical, Logical and Relational
| Symbols | Functions             |
| ------- | --------------------- |
| +       | Addition              |
| -       | Subtraction           |
| *       | Multiplication        |
| /       | Division              |
| %       | Remainder             |
| !       | Not                   |
| \|\|    | Or                    |
| &&      | And                   |
| ==      | Equals                |
| =       | Assign                |
| >       | Greater than          |
| <       | Less than             |
| >=      | Greater than or Equal |
| <=      | Less than or Equal    |


## For Loops
Question!! ???
```java
for (int i = 0; i < 10, i++){
	System.out.println(i)
}
```

Why does this output only 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 and without 10???
Simple, when `i == 10`, in the conditional phase, 10(i) is not less than 10 therefore our loop will break before 10 is  printed out from the loop.

Another form of for loop is this
```java
int[] numbers = {1, 2, 3, 4, 5};

for (int i : numbers){
	System.out.println(i);
}
```