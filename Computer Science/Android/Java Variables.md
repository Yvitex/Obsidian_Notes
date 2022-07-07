---
aliases: [data type]
---
# Java Variables
Unlike [[Python Programming]] with dynamic typing feature, Java variables are static, meaning when we declare a variable as a **String**, it could only accept a string and not an integer similar to the [[Mongoose Create Operations]] when creating a schema

(Note: *Variables* are simply containers that occupies a memory, like a volume of a [[Matter is anything that has space and weight|matter]] that occupies space in reality)

```java
String name = "Workdo-kun";

System.out.println("Hello " + name + " and Welcome" );
```

![[Pasted image 20220617040831.png]]

Sadly, there is no better way to modify a string but through concatenation. Unlike pythong with *f_string* or javascript with *template literals*

But there are also many merits in this type of feature which promotes better control over memory. Here are the different types of data types and their memory capacity

## Data Types and Capacity
Data types defines the type of operation we could use in a variable.

- Boolean (boolean) - 8 bits - either 0 or 1 ([[Switching Operation]])
- Byte (byte) - 8 bits - `[-128< byte > 127]` which is weird because [[IP Adress|8bits == 255]]
- Short (short) - 16 bits - `[-290 < byte > 289]` another weird one, 2 * 127 == 254
- Integer (int) - 32 bits
- Long (long) - 64 bits
- Float (float) - 32 bits 
- Double (double) - 64 bits more accurate than float
- Character (char) - 16 bits
- String (String) - depends on the amount of char

### In Table
| Data Type | Memory | Range         |
| --------- | ------ | ------------- |
| Boolean   | 1 byte | 0 and 1       |
| Byte      | 1 byte | -128 to 127   |
| Short     | 2 byte | -290   to 289 |
| Character | 2 byte |               |
| Integer   | 4 byte |               |
| Float     | 4 byte |               |
| Long      | 8 byte |               |
| Double    | 8 byte |               |
| String    | It depends       |               |


also. using long and float data type requires a symbol such as
```
long number = 100002020293L;
```

and
```
float decimal = 1.32f;
```

Double on the other hand does not require it as decimals default into double. 
Char on the other hand is enclosed with a single quote
```
char letter = 'A';
```

## Data Type Categories
| First Categories | Second Categories |
|:----------------:|:-----------------:|
|     Boolean      |      Numeric      |
|       Char       |      - byte       |
|                  |      - short      |
|                  |       - int       |
|                  |      - long       |
|                  |  Floating Point   |
|                  |      - float      |
|                  |     - double      |

All of the data types in the table are called [[Primitive Types]], string on the other hand is a non primitive data type or [[Reference Type]]
- Primitive types are fixed in size
- [[Reference Type]] are dynamic in size

The complexity now lies in the [[Java TypeCasting|operation]]s available for us to use, 