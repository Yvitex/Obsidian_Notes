# How to read a potentiometer
Here we cannot use [[Digital Pin]] but we use something such as an [[Analog Input Pin]] . The [[Arduino]] is said to b enot good at creating [[Analog Output Pin|true analog output]] but could be simulated using [[Analog Output Pin|pulse width modulation]]/ Aside from that fact, [[Arduino]] are good at reading analog input

In this example. we will use a [[Potentiometer]],![[Pasted image 20220701051949.png]]

The pins at the right side reads the [[Voltage Relationships in BJT|Vcc]], the left reads the [[Ground]] and the middle measures the [[Voltage]]
The schematic symbol for this is![[Pasted image 20220701052155.png]]
When we turn the potentiometer, the representation arrow moves to either 1 or 3. Imagine when 5v is connected to 3, what will happen if the arrow is on 3. That's right, as the resistance decrease, the voltage also decrease, remember the [[Ohm's Law]]?
$$V = IR$$
[[Voltage ]] is directly proportional to [[Resistance]]. The reverse will happen if the arrow is near 1, the voltage will increase. 

## In Code
For an instance that this is our circuit where the [[Analog Input Pin]] used is 0


```cpp
void setup(){
	Serial.begin(9600);
}

void loop(){
	Serial.println(analogRead(0))
}
```

```ad-Danger
title: Doesn't need a mode??
collapse: open
In analog input pins, we do not need to declare the mode as analog pins is readily declared as input. [[Analog Output Pins]] are declared in a different ports, with tilda sign

```
![[Pasted image 20220701053148.png]]

When we turn the potentiometer, ![[Pasted image 20220701053218.png]]

The maximum value is 1024 as the analog reading resolution is 10 bits, 2 ^ 10 = 1024

Now that we knew about this, time to modify the brightness of the [[LED]] in [[Modifying Brightness of LED using Potentiometer]]
