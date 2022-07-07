# UV Sensor
Used to detect the index of UV light in [[Arduino]]
Different products have different specification. In this case, what we will use is [GUVA S-12SD](https://www.adafruit.com/product/1918) UV sensor device. 

![[Pasted image 20220704103501.png]]

The first thing to look for is the responsivity in nano meter. We could see that in this graph, the reactivty starts from 240nm, but what we are interested at is the range in the center. It must be 280nm - 350nm. Information above is stated in the [GUVA S-12SD Documentation](https://cdn-shop.adafruit.com/datasheets/1918guva.pdf) 

So browsking in the [wikipedia](https://en.wikipedia.org/wiki/Ultraviolet), there are different subtypes of ultraviolet rays
![[Pasted image 20220704104035.png]]

Our type falls into the ultraviolet B subtype or UVB

According to the product specification in [GUVA S-12SD](https://www.adafruit.com/product/1918), to get the UV index of this sensor, we could devide the voltage by 0.1v.

[UV index](https://www.epa.gov/sunsafety/uv-index-scale-0) info could be found here
![[Pasted image 20220704110134.png]]

```cpp
void setup(){
	Serial.begin(9600);
}

void loop(){
	int sensorValue = analogRead(0);
	Serial.print("Sensor Value: ");
	Serial.println(sensorValue);
	float voltage = sensorValue * (5 / 1023);
	Serial.print("UV Index: ")
	Serial.println(voltage/0.1);
	
}
```

This will detect the UV index. First is we detect the sensorValue, then conver the sensorValue as a [[voltage]], divide it by 0.1 to get the UV index. 

The schematics for the above is
![[Pasted image 20220704112010.png]]



