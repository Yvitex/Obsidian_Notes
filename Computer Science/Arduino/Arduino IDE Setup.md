# IDE Setup
Here is the download website of [Arduino IDE](https://www.arduino.cc/en/software)

## Setup
- Tick number lines on
- Tick all verbose output setting
- Select the save file location
- Verify code after upload.
- Show all compiler warning. 
- Enable code folding
- Kepp default.
![[Pasted image 20220628060040.png]]

## Testing
- Connect the arduino to the computer
- Go to open > basics > blink
![[Pasted image 20220628055455.png]]

```cpp
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalWrite(LED_BUILTIN, HIGH);   // turn the LED on (HIGH is the voltage level)
  delay(1000);                       // wait for a second
  digitalWrite(LED_BUILTIN, LOW);    // turn the LED off by making the voltage LOW
  delay(1000);                       // wait for a second
}
```

Now, we could [[Arduino Programming|print]] how the arduino is doing.

```ad-Notice
title: Hello World?
collapse: open
This process is similar to the "Hello World" we do in software development. In this case, it is used to command the arduino board to blink

```
- In tools, ensure that the board you are using is an arduino uno or any board where you will upload it
![[Pasted image 20220628055705.png]]

- Now select the appropriate port depending on what arduino you connected
 ![[Pasted image 20220628055802.png]]

- We could choose get board info for information,
- Next is press upload. This will upload various things inside the console.
![[Pasted image 20220628055920.png]]

