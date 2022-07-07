# DHT22
Read the technical specification [here](https://www.sparkfun.com/datasheets/Sensors/Temperature/DHT22.pdf). 
![[Pasted image 20220704165158.png]]

Keep in mind the duration for the sensing period is 2 seconds, this is important so that we could get a more accurate reading. Patience is wisdom, bitch. Also we could also see that the accuracy is just ok but not very accurate. 

To attach our DHT22 temperature and humidity sensor, Here is the schematic.

![[2.1 0430 - DHT22.png.png]]

We, once again make a [[Pull Up or Down Resistor|pull-up]] resistor that will be the default value when there is no direct input from the [[Digital Pin]]. The [[Pull Up or Down Resistor|pull-up]] resistor is connected to the [[Voltage Relationships in BJT|Vcc]] but also is the Vin or the left pin, the right pin is connected to the [[Ground]]

![[Pasted image 20220704165719.png]]

In our code, we will use the [DHT Sensor Library](https://github.com/adafruit/DHT-sensor-library) 
```cpp
#include "DHT.h"
```

Next is we define the pin we used and the DHT tye of our material
```cpp
#define DHTPIN 2
#define DHTTYPE DHT22 //our device is dht22
```

Next is we merge this 2 defined vlaue into one variable
```cpp
DHT dht(DHTPIN, DHTTYPE);
```

Next, in our setup is just initiating the Serial monitor and also starting the sensor
```cpp
void setup(){
	Serial.begin(9600);
	Serial.println("Start");
	dht.begin();
}
```

As the technical specification declares, the reading functions properly per 2 seconds. Therefore in our loop, we set the delay before each process a 2 second interval
```cpp
void loop(){
	delay(2000);
}
```

We could get the himidity by using the `readHumidity()` method and the temperature using `readTemperature()`
```cpp
void loop(){
	delay(2000);
	float h = dht.readHumidity();
	float t = dht.readTemperature(); //in celcius default
	float f = dht.readTemperature(true); //in farensheight, farenheight = true
}
```

We could also check if there is an error in our values, then exit, then execute the loop again.
```cpp
void loop(){
	delay(2000);
	float h = dht.readHumidity();
	float t = dht.readTemperature(); //in celcius default
	float f = dht.readTemperature(true); //in farensheight, farenheight = true

	if(isnan(h) || isnan(t) || isnan(f)){
		Serial.println("There is an error fetching data");
		return;
	}
}
```

We could also compute for the heatindex which is the heat we feel, not the actual temperature.
```cpp
void loop(){
	delay(2000);
	float h = dht.readHumidity();
	float t = dht.readTemperature(); //in celcius default
	float f = dht.readTemperature(true); //in farensheight, farenheight = true

	if(isnan(h) || isnan(t) || isnan(f)){
		Serial.println("There is an error fetching data");
		return;
	}

	float hif = dht.computeHeatIndex(f, h); // default in farenheight
	float hic = dht.computeHeatIndex(t, h, false) // in farenheight = false; celcius
}
```

Now we could print this data
```cpp
#include "DHT.h"

#define DHTPIN 2
#define DHTTYPE DHT22 //our device is dht22

DHT dht(DHTPIN, DHTTYPE);

void setup(){
	Serial.begin(9600);
	Serial.println("Start");
	dht.begin();
}

void loop(){
	delay(2000);
	float h = dht.readHumidity();
	float t = dht.readTemperature(); //in celcius default
	float f = dht.readTemperature(true); //in farensheight, farenheight = true

	if(isnan(h) || isnan(t) || isnan(f)){
		Serial.println("There is an error fetching data");
		return;
	}

	float hif = dht.computeHeatIndex(f, h); // default in farenheight
	float hic = dht.computeHeatIndex(t, h, false) // in farenheight = false; celcius

	Serial.print("Humidity: ");
	Serial.print(h);
	Serial.print(" %\t");
	Serial.print("Temperature: ");
	Serial.print(t);
	Serial.print(" *C ");
	Serial.print(f);
	Serial.print(" *F\t");
	Serial.print("Heat index: ");
	Serial.print(hic);
	Serial.print(" *C ");
	Serial.print(hif);
	Serial.println(" *F");

}
```
