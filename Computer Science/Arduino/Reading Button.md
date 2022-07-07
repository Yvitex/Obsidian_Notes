# Reading Button
## Setup
First is we check the connection between buttons using [[Multimeter]]'s contuinity functionality. We connect the pin to one side of the button to a [[Digital Pin]] which is connected to a [[Resistor]] connected to the [[Ground]] the other side is connected to the [[Voltage Relationships in BJT|Vcc]], this configuration will avoid a [[Hanging Value|float]] or hanfing value and this case, our resistor is not used for protection but for [[Pull Up or Down Resistor|pull-down]] resistance. 

![[Pasted image 20220701044225.png]]

![[Pasted image 20220701044240.png]]


## Code to Read
First is to set the [[Digital Pin]] to Input
```cpp
void setup(){
	pinMode(2, INPUT);
	Serial.begin(9600);
}
```

Create a global variable that will store the state of the button
```cpp
int buttonState = 0;

void setup(){
	pinMode(2, INPUT);
	Serial.begin(9600);
}
```

In the loop. we will assign our variable into the actual state of button with if else statement.
```cpp
int buttonState = 0;

void setup(){
	pinMode(2, INPUT);
	Serial.begin(9600);
}

void loop(){
	buttonState = digitalRead(2);
	if(buttonState == HIGH){
		Serial.println("High");
	}
	else{
		Serial.println("Low");
	}
}
```

![[Pasted image 20220701051228.png]]

This will repeatedly print low until we press the button

