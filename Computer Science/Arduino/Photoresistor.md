# Photoresistor
Is also called as photocell or light dependent [[Resistor]] which is a type of [[Semiconductor]]. How it is dependent? Well, when there is no light, the [[Resistance]] of this resistor goes up but when there is a light hitting on the surface of the resistor, then the resistance goes down. And because the [[Resistance]] goes down and so is the [[Voltage]]. Remember the [[Ohm's Law]]?
$$V = IR$$
Resistance is directly propotional to the voltage. To make use of it, we must utilize the art of contructing a [[Voltage Divider]] the same on how the builtin contruct of a [[Potentiometer]] is constructed.

![[Pasted image 20220704053932.png]]

The midpoint between the 2 [[Types of Electric Circuit|series]] resistor will be the one that will output the analog value to the [[Analog Input Pin]] 
![[Pasted image 20220704054047.png]]

In code, we may read this as
```cpp
void setup(){
	Serial.begin(9600);
}

void loop(){
	int photoResVal = analogRead(0);
	Serial.println(photoResVal);
}
```

![[chrome-capture-2022-6-4.gif]]

As we could see, the brighter it is, the less the resistance. 

Now, the greatest question to ask is how we could choose the corrent fixed resistance for our photoresistor, now, in our [[Voltage Divider]] formula, we have 2 kinds of formula that will calculate the [[Voltage]] of each component. But in a more general case, we use this formula $$v_{out} = \frac{Z_2}{Z_1 + Z_2} v_{in}$$

We also need to measure the resistance of the photoresistor in normal light condition![[chrome-capture-2022-6-4 (1).gif]]

Our Given is the following
- $V_{in} = 5v$
- $V_{out} = 2.5v$ (must be as we wanted the output to be one hald the [[Vcc]])
- $Z_2 = 781 \ohm$   is the resistance of photoresistor in the normal light condition.

$$2.5v = \frac{781 \ohm}{Z_1 + 781 \ohm}\times 5v$$
In this case. $Z_1 = 781 \ohm$ .

In conclusion, we choose the fixed resistor by simple looking for the normal light condiction, the value of the normal light condiction will also be the value of our fixed resistor. 