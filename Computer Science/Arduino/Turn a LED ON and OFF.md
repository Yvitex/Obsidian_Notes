# Turning the LED ON and OFF using Arduino
In this example, we are using a red [[LED]], a [[Resistor]], [[Arduino]], a [[Breadboard]], jumper wires,

### In Diagram
![[Drawing 2022-06-28 16.24.03.excalidraw.png]]


### In RL

![[Pasted image 20220628162851.png]]


```ad-Notice
title: Notice
collapse: open
We could set the resistor (220 ohms) to either side of the polarities of LED. Don't forget to set it or else it might explode or some cool shit

```


To activate the LED light... We first set the [[Digital Pin]] no 8 where we have our anode set up. 
```cpp
void setup(){
	pinMode(8, OUTPUT);
}
```

Because we are usign our digital pin 8 to an output component, then we set it to `OUTPUT` rather than `INPUT`
Next step is to create a loop where we try to let the LED blink by setting the [[Digital Pin]] 8 into high then low at an interval. 
```cpp
void loop(){
	digitalWrite(8, HIGH);
	delay(1000);
	digitalWrite(8, LOW);
	delay(1000);
}
```

```ad-Notice
collapse: open
It seems like all the method are written in camel-casing at c++

```

