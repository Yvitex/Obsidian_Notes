---
aliases: [acceleration sensor, accelerometer]
---
# ADXL 335
## Datasheet
Here are the datasheet for [adxl 335](https://www.analog.com/media/en/technical-documentation/data-sheets/ADXL335.pdf)

## Basics
![[Pasted image 20220713152325.png]]

Accelerometer could detect the orientation in the 3 axis, acceleration etc. It only need low power [[Electric Current|Current]] in 350 micro amphere but as we could see, the voltage supply that we need is low therefore, becareful when plugging [[Voltage]] in the device without a breakout, [[Resistor]] or plug it on the 3.3 voltage supply [[Switching to 3v Vcc]]
![[Pasted image 20220713152629.png]]

We could see that the measurement range is $\pm3.6g$  where 1g is the acceleration of an object to the center of the earth, well 9.8 m/s^2 if I am correct? In the sensitivity section, it is said that the typical measruement is 300mV/g or in 1g, there is a 300mV of [[Voltage]] plus the Zerog bias level of 1.5V
This means that when the sensor is placed on a table without motion, then it will have a normal force which is the only force interacting with is gravity equivalent to 1g. And 1g is equals to $1.5v + 300mV$

## Wiring
### Version 1
![[2.2 0520 - ADXL335 accelerometer 2.png.png]]

THis is the normal type of wiring where we connect the device to the 3.3 v. We are [[Switching to 3v Vcc]]
We connect the [[Analog Input Pin]] 2, 3 and 4 to the analog 1 , 2  and 3 but it depends. Then the usual connection,

### Version 2
![[3.1 0520 - ADXL335 accelerometer 1.png.png]]

This version directly attaches to the [[Arduino]]. This is only possible is we make [[Analog Input Pin]] 4 as [[Ground]] and 5 as [[Voltage Relationships in BJT|Vcc]] by setting them to high or low. See, [[Analog Input Pin]] do not just read voltage but it also create [[Voltage]]

## Code
### Version 1
This is for those sensor without voltage regulator
First of all, define all pins we used to the orientation axis 
```cpp
int x_axis = 3;
int y_axis = 2;
int z_axis = 1;
```

Create variable that will hold the output values in the xyz axis
```cpp
int x_axis = 3;
int y_axis = 2;
int z_axis = 1;

int x, y, z;
```

Start the Serial monitor and set the `analogReference` to extenal
```cpp
int x_axis = 3;
int y_axis = 2;
int z_axis = 1;

int x, y, z;

void setup(){
	Serial.begin(9600);
	analogReference(EXTERNAL);
}
```

Read each analog values and print it out
```cpp
int x_axis = 3;
int y_axis = 2;
int z_axis = 1;

int x, y, z;

void setup(){
	Serial.begin(9600);
	analogReference(EXTERNAL);
}

void loop(){
	x = analogRead(x_axis);
	y = analogRead(y_axis);
	z = analogRead(z_axis);

	Serial.print(x);
	Serial.print("\t");
	Serial.print(y);
	Serial.print("\t");
	Serial.print(z);

	delay(100);
}
```

### Version 2
Available for those who have voltage regulator.
We initialize the xyz axis
```cpp
int x_axis = A3;
int y_axis = A2;
int z_axis = A1;

int x, y, z;
```

Next is to initialzie te [[Analog Input Pin]] 4 and 5 as ground and source
```cpp
int x_axis = A3;
int y_axis = A2;
int z_axis = A1;

int x, y, z;

int ground = A4;
int source = A5;
```

Setup the serial monitor and make the [[Analog Input Pin]] 4 and 5 as high or low
```cpp
int x_axis = A3;
int y_axis = A2;
int z_axis = A1;

int x, y, z;

int ground = A4;
int source = A5;

void setup(){
	Serial.begin(9600);

	pinMode(ground, OUTPUT);
	pinMode(source, OUTPUT);

	digitalWrite(ground, LOW);
	digitalWrite(source, HIGH);

	delay(1000);
}
```

Next is to output the xyz orientation
```cpp
int x_axis = A3;
int y_axis = A2;
int z_axis = A1;

int x, y, z;

int ground = A4;
int source = A5;

void setup(){
	Serial.begin(9600);

	pinMode(ground, OUTPUT);
	pinMode(source, OUTPUT);

	digitalWrite(ground, LOW);
	digitalWrite(source, HIGH);

	delay(1000);
}

void loop(){
	x = analogRead(x_axis);
	y = analogRead(y_axis);
	z = analogRead(z_axis);

	Serial.print(x);
	Serial.print("\t");
	Serial.print(y);
	Serial.print("\t");
	Serial.print(z);

	delay(100);
}
```



