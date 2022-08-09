# How to change address
We can change the address of [[Two Wire Interface]], in this example. we will use the beloved [[MCP9808]] for study sake

In the [[Read Datasheet and C++ Library|datasheet]] of this [Device](https://ww1.microchip.com/downloads/en/DeviceDoc/25095A.pdf) we could see the address pin information
![[Pasted image 20220713061243.png]]

The first row is the main, we could ee that [[Analog Input Pin]] A3 to A6 is already fixed leaving the A0 to A2 with default 0 values that can be changed simply by applying a [[Voltage Relationships in BJT|Vcc]] to it. THis is just the basics of [[Switching Operation]]. 

So the default address in [[Binary]] is 0011000 which is in [[Hexadecimal Notation]] will be 0x18. We could use a converter such as this [Binary to hex Converter](https://www.rapidtables.com/convert/number/binary-to-hex.html) 

When we apply a [[Voltage Relationships in BJT|Vcc]] to the A0 [[Analog Input Pin]], it will become 0011001 which is converted into [[Hexadecimal Notation]] 0x19. Therefore the address to be inputed into the code is **0x19**

Using the [[Read Datasheet and C++ Library|arduino library]] of [MCP9808](https://github.com/adafruit/Adafruit_MCP9808_Library) from adafruit, we could see that inside the .h file, the default address is set to 0x18
![[Pasted image 20220713062051.png]]

We also have parametered non default `begin()` method
![[Pasted image 20220713062257.png]]


Then we could set it up like
```cpp
temSensorObj.begin(0x19);
```

We could use this scanner to [detect the address of device easily](https://github.com/futureshocked/ArduinoSbS2017/blob/master/i2c_scanner/i2c_scanner.ino)
