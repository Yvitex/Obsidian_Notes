# Arrays
Arrays are collection of element of similar [[C++ Data Types]]. The syntax goes like...

```cpp
int number[] = {1, 2, 3, 4, 5};
```

In character set, we could do this in 3 ways/
```cpp
char letter[] = {'a', 'b', 'c', 'd', 'e'};
char letter[6] = {'a', 'b', 'c', 'd', 'e'};
char letter[6] = "abcde";
```

6 is the length of the element plus 1.  The third syntax is the same as the above, a string value will be converted to individual character as commanded. 

We could create array without adding any value
```cpp
char letter[6];
```

We can access the value in each container individually by specifying their index
```cpp
Serial.println(letter[0]);
```

We could also update it in the same way
```cpp
letter[0] = 'z';
```

