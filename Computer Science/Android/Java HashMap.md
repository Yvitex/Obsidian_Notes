# HashMap
Similar to [[Javascript]] objects and [[Python]]'s dictionary
## Documentation
Here is the documentation of [Hashmap](https://docs.oracle.com/en/java/javase/18/docs/api/java.base/java/util/HashMap.html)

## Basics
Import the module
```java
import java.util.HashMap;
```

The syntax needs to declare the key and value data types such as
```java
HashMap<String, Integer> famFriendly = new HashMap<>();
```

Key is of type String nad value is of type Integer, both in class form not in primitive.
To add values, we could use the method `put`

```java
famFriendly.put("Oreimo", 10);
famFriendly.put("Yosuga no Sora", 5);
famFriendly.put("Sister Testament", 10)
```

We could print the keys and value pair by simply raw printing it.
```java
System.out.println(famFriendly);
```
![[Pasted image 20220711090625.png]]

We could print the key out using the `keySet` in an array
```java
System.out.println(famFriendly.keySet());
```
![[Pasted image 20220711090730.png]]

We could also print the values out
```java
System.out.println(famFriendly.values());
```
![[Pasted image 20220711090808.png]]

```ad-Danger
title: Fuckin Bitch
collapse: open
We cannot use a loop to modify the values of the hashmap. It will give of an error

```
![[Pasted image 20220711091046.png]]
