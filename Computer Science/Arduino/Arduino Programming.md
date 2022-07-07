# Arduino Programming
## Big Topics
[[Arduino Programming Basic Setup]]
[[How to print to the console from Arduino]]
[[Creating Custom Function in Arduino]]
[[C++ Data Types]]
[[Turn a LED ON and OFF]]
[[Reading Button]]
[[Reading a Potentiometer]]
[[Modifying Brightness of LED using Potentiometer]]
[[Using RGB LED in Arduino]]

## Special Methods
Some of the methods used often
### Delay Time
```cpp
delay(1000) // in milliseconds
```

### Count the Miliseconds After Upload
```cpp
void loop(){
	Serial.println(millis());
	delay(1000);
}
```

### Set Pins to Output or Input
```cpp
pinMode(8, OUTPUT);
```

### Digital Write
Set a pin to high or low.
```cpp
digitalWrite(8, HIGH);
```

### Serial Read
Will read user input and store it into a variable
```cpp
char something = Serial.read()
```
## ASCII
```cpp
Serial.println('a', DEC);
```

## Char False Concat
```cpp
Serial.println('a' + 'b');
```

Output: 195
proof: ![[Pasted image 20220701164850.png]]
It was added by their ASCII decimal

## Accidental Truncation
```cpp
char a = 'a';
char z = 'z';
char total = a + z;
Serial.println(total, DEC);
```

Output: -37
```ad-Danger
collapse: open
Remember [[C++ Data Types]], have specific memory storage size, so when we create a data type that could hold small amount of storage, for example is a char that could hole a maximum of 256, then a + z which is 97 + 122 = 219. And 219 - 256 = -37. Which is why this is our output

```

### Length
We use the `sizeof` method
```cpp
for(int i = 0; i < sizeof(items); i++){

}
```

## Techniques
### Wait for the serial monitor
This will wait until serial monitor is open before printing something.
```cpp
while(!Serial){
	;
}
```

### Wait for user to type something
Will wait until user type something in the keyboard
```cpp
while(Serial.available() == 0){

}
```











Additional Information in the Official Website's [Documentation](https://www.arduino.cc/reference/en/)
