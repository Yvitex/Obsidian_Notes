# ArrayList
## Documentation
[ArrayList](https://docs.oracle.com/en/java/javase/18/docs/api/java.base/java/util/ArrayList.html)

## Basics
A more flexible [[Data Structure]] that is similar to [[Java Arrays]]. We could add, delete data as we do not need to lock the list with a fixed length
```java
ArrayList flexible = new ArrayList();
```

This syntax will prompt us to use an import, unlike Arrays
```java
import java.util.ArrayList;

ArrayList flexible = new ArrayList();
```

Now we could add any data type values using the `add()` that accepts any [[Java OOP Inheritance|superclass]] object, meaning anything
```java
import java.util.ArrayList;

ArrayList flexible = new ArrayList();
flexible.add("Hello World");
flexible.add(44);

System.out.println(flexible);
```
![[Pasted image 20220711044454.png]]

We could also delete vlaues using the values it self
```hava
import java.util.ArrayList;

ArrayList flexible = new ArrayList();
flexible.add("Hello World");
flexible.add(44);

flexible.remove("Hello World");

System.out.println(flexible);
```
![[Pasted image 20220711044643.png]]

or using index. We could also modify the arrayList to only contain a fixed set of data types
```java
import java.util.ArrayList;

ArrayList<String> flexible = new ArrayList<>();
```

This will cause an error if we add an integer.
To print the values, the typical syntax `flexible[i]` will not cut it but because we are workign with an object, and guess what? [[Getter and Setter in Java]], we will utilize this priniple to get the data on the index throught he `get()` method
```java
int i;
for(i = 0; i< flexble.size(); i++){
	System.out.println(flexible.get(i));
}
```

## Methods
### Add
```java
ArrayList flexible = new ArrayList();
flexible.add("Hello World");
flexible.add(44);
```

### Remove
Remove item from the list
```java
ArrayList flexible = new ArrayList();
flexible.add("Hello World");
flexible.add(44);

flexible.remove("Hello World");
```

### Size
Get the length of the arrayList as length won't work
```java
flexible.size();
```

## For Each
Iterate for each item in the variable arrayList,
```java
flexible.forEach((n) -> System.out.println(n));
```
