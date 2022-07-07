## How to print to the console from Arduino?
We could do this, but first, inside the setup, we must tell that we want to send  data from arduino to the IDE with the syntax `Serial.begin(9600)` that will enable the serial monitor the argument is the speed. 

```cpp
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
  Serial.begin(9600)
}
```

Next is what we wanted to print and we do this inside the loop. 
```cpp
// the loop function runs over and over again forever
void loop() {
  digitalWrite(LED_BUILTIN, HIGH);   // turn the LED on (HIGH is the voltage level)
  delay(1000);                       // wait for a second
  Serial.println("ON")
  digitalWrite(LED_BUILTIN, LOW);    // turn the LED off by making the voltage LOW
  delay(1000);                       // wait for a second
  Serial.println("OFF")
}
```

Inside tools, in the Serial monitor, we may see this
![[Pasted image 20220628104930.png]]

Remember that the Serial Monitor must match the speed we applied as an argument to the `Serial.begin()` method.

If we set it up as a value like this
```cpp
void loop() {
  digitalWrite(LED_BUILTIN, HIGH);   // turn the LED on (HIGH is the voltage level)
  delay(1000);                       // wait for a second
  Serial.println(1)
  digitalWrite(LED_BUILTIN, LOW);    // turn the LED off by making the voltage LOW
  delay(1000);                       // wait for a second
  Serial.println(0)
}
```

Then we could use the  Serial plotter
![[Pasted image 20220628105201.png]]


To simplify this out,
```cpp
void setup(){
	Serial.begin(9600);
	Serial.println("Hello World");
}
```

Will print "Hello World" in the Serial Monitor Once and,
```cpp
void loop(){
	Serial.println("Hello World");
	delay(1000)
}
```

Will print "Hello World" Endlessly for every 1 second delay