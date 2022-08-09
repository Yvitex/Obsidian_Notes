---
aliases: [steinhart-hart equation, ADC]
---

# Thermistor
![[Pasted image 20220709130147.png]]
Is a type of [[Resistor]] that measures temperature depending on resistance, kinda like [[Temperature and Humidity Sensor|dht22]] but can't detect humidity or autmaticallly calculat eht heat index. Here are the articles about [thermistor](https://en.wikipedia.org/wiki/Thermistor). 

There are 2 types of resistor. 
- NTC - negative temperature coefficient - temperature is inversely proportional to [[Resistance]]
- PTC - positive temperature coefficient - temperature is directly propotional to resistance

$$NTC = T = 1/R$$
$$PTC = T = R$$

## Steinhart - Hart Equation
An equation model used for approximating resistance at different temperatures or resistance - temperature conversion. This is effective over a range of temperature in contrast to the linear model I don't have any idea about

## Calculation
![[Drawing 2022-07-09 11.53.10.excalidraw.png]]

This is also how we use a thermistor in an [[Arduino]], the same as [[Photoresistor]]. This is called [[Voltage Divider]] so therefore
$$V_{out} = V{in}\frac{R_2}{R_1 + R_2}$$
Then we couvert the output to the proper version inside arduino 
$$ADC = V_{out} \frac{1023}{V_{in}}$$
So messing this 2 equation we have $$ADC = V_{in}\frac{R_2}{R_1 + R_2} \times \frac{1023}{V_{in}}$$
Simplify and $$ADC = \frac{R_2}{R_1 + R_2} \times {1023}$$
In simplified form $$R_2 = \frac{R_1}{\frac{1023}{ADC} - 1}$$
Also ADC means analog to digital converter which is the reading from the thermistor.

## Construction
![[Pasted image 20220709123048.png]]

The same as [[Photoresistor]]
![[4.2 0440 - Thermistor 5V.png.png]]

Theremistor is a [[Analog Input Pin]] device
## Code
### For Thermistor Resistance
Already shown above the formula. 
Definte the given. The following is only the pin and the fixed [[Resistor]] [[Resistance]]
```cpp
#define THERMISTORPIN A0
#define FIXEDRESISTOR 9950
```

Next is to read the thermistor pin
```cpp
#define THERMISTORPIN A0
#define FIXEDRESISTOR 9950

int reading;

void setup(){
	Serial.begin(9600);
}

void loop(){
	reading = analogRead(A0);

	Serial.print("Analog reading: ");
	Serial.println(reading);
}
```

We could convert it using the formula above where we convert the reading (ADC) and to thermistor resistance
```cpp
#define THERMISTORPIN A0
#define FIXEDRESISTOR 9950

int reading;

void setup(){
	Serial.begin(9600);
}

void loop(){
	reading = analogRead(A0);

	Serial.print("Analog reading: ");
	Serial.println(reading);

	reading = (1023 / reading) - 1;
	reading = FIXEDRESISTOR / reading;
	Serial.print("Thermistor Resistance: ");
	Serial.println(reading);

	delay(1000);
}
``` 

To get the actual temperature, we need and algorithm resistance to temperature conversion using the steinhart hart equation yeah. So we need a propert library like [thermistor](https://github.com/panStamp/thermistor).

An example of its implementation can be found [here](https://github.com/panStamp/thermistor/blob/master/examples/basicntc/basicntc.ino)
```cpp
#include "thermistor.h"

#define TH_PIN A0
```

We then create an object thermistor that will read the data
```cpp
#include "thermistor.h"

#define TH_PIN A0

THERMISTOR thermistor(TH_PIN,
					  1000,
					  3950,
					  10000
					  )
```

Ther parameters above is the pin to read, second is the resistance at 25 degree celcius, third is thermistor beta coefficient and last one is the resistance from the fixed resistor.

We will then read the thermistor per 5 seconds
```cpp
#include "thermistor.h"

#define TH_PIN A0

int reading;

THERMISTOR thermistor(TH_PIN,
					  1000,
					  3950,
					  10000
					  )
void setup(){
	Serial.begin(9600);
}

void loop(){
	reading = thermistor.read();
	Serial.print("Thermistor termperature: ");
	Serial.println(reading);

	delay(5000);
}
```

THis is not perfect and need to be calibrated like the fixed resistor resistance and the resistance at 25 degree centigrade.

```ad-Danger
title: Not accurate enough
collapse: open
In [[Arduino]], there are a lot of noise in the 5v power supply. This will hinder the accuracy of the ADC value
```

What we could do is to consider [[Switching to 3v Vcc]]








