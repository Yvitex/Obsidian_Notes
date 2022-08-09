# TMP36
Another [[Temperature and Humidity Sensor|temperature sensor]].
![[Pasted image 20220709150741.png]]

Working with tmp36 wil require us to find the markings then connect the circuitry based on it.
Here is the [datasheet regarding tmp36](http://www.analog.com/media/en/technical-documentation/data-sheets/TMP35_36_37.pdf)
![[Pasted image 20220709150927.png]]

Analyzing the features we could see it is adaptable tot he [[Arduino]] supply. It is mreasured directly in centigrafe and its accuracy have a positive negative 2 in centigrade. As well as the linearity with 0,5 degree offset.

## Linearity
[[Linearity]] looks like this
![[Pasted image 20220709152038.png]]

It is just a linear equation between the measured value and the voltage. This also exit in other components like [[Thermistor]] which is somehow like [[Linear Regression]]. This makes the conversion from [[Voltage]] to the desired units easier.

We could see that tmp36 runs from negative temperature to 125 which is equivalent to greater than 1.6 to less tan 0.2 voltage.

## Setup
![[9.2 0450 - TMP36 Temperature sensor 5V.png.png]]

We could also do a 3.3 v source for [[Switching to 3v Vcc|clean reading]]

## Code
Set up the constant variables
```cpp
#define Analog 0
#define Source 5
```

Start the Serial board
```cpp
#define Analog 0
#define Source 5

void setup(){
	Serial.begin(9600);
}
```

Convert the raw data to voltage
```cpp
#define Analog 0
#define Source 5

void setup(){
	Serial.begin(9600);
}

void loop(){
	int readings = analogRead(Analog);
	Serial.print("Raw data: ");
	Serial.println(reading);

	int voltage = readings * (Source / 1023);
	Serial.print("Voltage Reading: ");
	Serial.println(voltage);
}
```

Conver the [[Voltage]] value to centrigrade by applying the offset and multiplying it by 100
```js
#define Analog 0
#define Source 5

void setup(){
	Serial.begin(9600);
}

void loop(){
	int readings = analogRead(Analog);
	Serial.print("Raw data: ");
	Serial.println(reading);

	int voltage = readings * (Source / 1023);
	Serial.print("Voltage Reading: ");
	Serial.println(voltage);

	int celcius = (voltage - 0.5) * 100;
	Serial.print("Cecius: ");
	Serial.println(celcius);

	delay(1000);
}
```

![[chrome-capture-2022-6-9.gif]]


Now, if you are using the 3.3 v as the voltage source
![[9.3 0450 - TMP36 Temperature sensor 3V3.png.png]]

Then we must set the `analogReference(EXTERNAL)` in the setup and source to 3.3
```cpp
#define Analog 0
#define Source 3.3

void setup(){
	analogReference(EXTERNAL);
	Serial.begin(9600);
}

void loop(){
	int readings = analogRead(Analog);
	Serial.print("Raw data: ");
	Serial.println(reading);

	int voltage = readings * (Source / 1023);
	Serial.print("Voltage Reading: ");
	Serial.println(voltage);

	int celcius = (voltage - 0.5) * 100;
	Serial.print("Cecius: ");
	Serial.println(celcius);

	delay(1000);
}
```