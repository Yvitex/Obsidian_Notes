# C++ Data Types
Here are the list of data types to consider;
| Data Type        | Code                 | Memory | Range                             |
| ---------------- | -------------------- | ------ | --------------------------------- |
| Boolean          | Boolean              | 1 byte | 0 and 1                           |
| Character        | char                 | 1 byte | -127 to 127                       |
| Byte             | byte                 | 1 byte | 0 to 255                          |
| Integer          | int                  | 2 byte | -32768 to 32767                   |
| Unsigned Integer | undesigned int/ word | 2 byte | 0 to 65535                        |
| Long Integer     | long                 | 4 byte | -2,147,483,648  to -2,147,483,647 |
| Unsigned Long    | unsigned long        | 4 byte | 0 to 4,294,967,296                |
| Float            | float                | 4 byte | -3.402823466 E^38 to 3.402823466 E^38                                  |

## How to Create a Variable?

Compare it to [[Java Variables]]

Setting a varible works like
```cpp
int number = 5;

void setup(){
	Serial.begin(9600);
	Serial.println(number)
}
```

## Constant
To set a variable to constant, we just add the keyword `const` such as
```cpp
const int number = 5;

void setup(){
	Serial.begin(9600);
	Serial.println(number)
}
```