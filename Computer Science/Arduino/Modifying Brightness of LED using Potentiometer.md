# How?
Adding some [[LED]] and [[Resistor]], to our component in the section at [[Reading a Potentiometer]]...
![[Pasted image 20220701103411.png]]

We connect the [[LED]] to the [[Ground]] and to the [[Analog Output Pin]]. In code we do this.
```js
void setup(){
	pinMode(6, OUTPUT);
}
```

We set the [[Analog Output Pin]] no 6 as an output port. Remember that the tilde sign is a sign of [[Analog Output Pin|pulse width modulation]] so even though it looks like a [[Digital Pin]], it is an [[Analog Output Pin]]

```js
void loop(){
	int potValue = analogRead(0);
	analogWrite(6, potValue);
}
```

```ad-Danger
title: Not working!!! Fucking hELL
collapse: open
This doesnot work because [[Analog Input Pin]] have a different maximum value, namely 1023 than [[Analog Output Pin]] which maximum is equivalent to 255

```
There fore we need to map it straight. 
```js
void loop(){
	int potValue = analogRead(0);
	int convertedVal = map(potValue, 0, 1023, 0, 255);
	analogWrite(6, potValue);
}
```

Map method accepts 5 arguments, first is the value to be converted, second and third is the maximum and minum value of the first parameter and the second is the maximum and minum it will be converted at.

This effect will cause the LED to fade, trust me... I deleted the simulation. 


Related: [[Analog Input Pin]], [[Analog Output Pin]]