# RGB Sensor Module
![[Pasted image 20220704115107.png]]

This is an image of [TCS34725](https://ams.com/documents/20143/36005/TCS3472_DS000390_3-00.pdf/6fe47e15-e32f-7fa7-03cb-22935da44b26) rgb sensor. The main sensor is located at the middle ![[Pasted image 20220704115413.png]]
Acmpanied by a white [[LED]] for a more accurate reading to the color.![[Pasted image 20220704115707.png]]
We could also control this [[LED]] for by controlling this pin![[Pasted image 20220704115652.png]]
The sensor contain 4 by 3 photodiode. One for red, then green, then blue color detection then a clear light sensing, all with infrared light filter times 3. There are 3 of each of those kind to compare their values to each other and create a more accurate reading. 

There are lot of application in using this sensor. Just read it in the documentation. 

To use this inside an [[Arduino]], we will attach it like this
![[Pasted image 20220704145747.png]]

We could see that this type of component make use of our [[Two Wire Interface]]'s SDA and SCL. It is connected to the specified pin in the arduino. The [[Ground]] and VIN is connected to the specified pin and also to the [[Voltage Relationships in BJT|Vcc]]. We could also connect the [[LED]] to the ground to turn the builtin [[LED]] in the sensor off. 

In our code, we will use the adafruit library for [tcs34725](https://github.com/adafruit/Adafruit_TCS34725).
First import is the Wire then the exact library to tcs
```cpp
#include <Wire.h>
#include <Adafruit_TCS34725.h>
```

The easiest way to import this are by going to sketch then include library![[Pasted image 20220704150949.png]]
We use the Wire library to support the [[Two Wire Interface]]

NExt is we set and configure the contructor
```cpp
Adafruit_TCS34725 tcs = Adafruit_TCS34725(TCS34725_INTEGRATIONTIME_50MS, TCS34725_GAIN_4X);
```

Adafruit contructor accepts 2 parameter, it and gain. 
Next thing to do is to check weather the sensor is detected or not. We do this through `.begin()` on the object `tcs`
```cpp
void setup(){
	Serial.begin(9600);
	Serial.println("Color Test");

	if(tcs.begin()){
		Serial.println("Sensor Found");
	}
	else{
		Serial.println("Sensor not found... check connection");
		while(1);
	}
}
```

`while(1)` will halt the codeif the sensor is not found.
Next, we will create 4 variables that will hold to the 4 values of red, green, blue and clear. Because we are trying to preserve memory, we will use an integer value that is atleast capavle of 16 bits of data, we do this by using `uint16_t`

```cpp
void loop(){
	uint16_t clear, red, green, blue;
}
```

Next is to set the sensor to prevent an interrupt, 
```cpp
void loop(){
	uint16_t clear, red, green, blue;
	tcs.setInterrupt(false);
}
```

Detecting colors takes at least 50ms to process so we could set the delay to at least 60ms
```cpp
void loop(){
	uint16_t clear, red, green, blue;
	tcs.setInterrupt(false);
	delay(60);
}
```

Then we could get the raw values by calling the method `.getRawData()`
```cpp
void loop(){
	uint16_t clear, red, green, blue;
	tcs.setInterrupt(false);
	delay(60);
	tcs.getRawData(&red, &green, &blue, &clear);
}
```

```cpp
void loop(){
	uint16_t clear, red, green, blue;
	tcs.setInterrupt(false);
	delay(60);
	tcs.getRawData(&red, &green, &blue, &clear);
	Serial.print("C:\t"); Serial.print(clear);
	Serial.print("\tR:\t"); Serial.print(red);
	Serial.print("\tG:\t"); Serial.print(green);
	Serial.print("\tB:\t"); Serial.print(blue);
}
```

The output will look like this
![[Pasted image 20220704155604.png]]

Depending on the color placed on the sensor, the vlaue of colors may increase, here are some table values
![[Pasted image 20220704155718.png]]