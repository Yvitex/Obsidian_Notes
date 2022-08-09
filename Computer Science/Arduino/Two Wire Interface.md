# TWI
Is a [[Half-duplex]] [[Communication Protocol]] and a [[Bus]] that mean **Two Wire Interface**. It is also called $I^2C$ or **Inter- Integrated Circuit**

This communication protocol can  be found at SCL and SDA as well as [[Analog Input Pin]] a4 and a5. 
- SCL and A5 is responsible for the CLOCK, for everyticks of the clock, the-
- SDA and A4 will send one bit per tick. 

```ad-Notice
collapse: open
Arduino Uno has a clock speed of 16Mhz or 16 million cycles per seconds. Though, Mega2560 also has a smilar clock speed so time dependent functionality will still work in upgrade.

```

This communication protocol can be used to chain components...
![[Drawing 2022-06-25 03.47.48.excalidraw.png]]

Unlike [[UART LLT Serial Communication]] that can only connect to one component at a time. 

TWi also exhibit a master-slave relationship where the arduino is the master and the components are the slave. Basically the arduino manages the slave component.

## Function
- It could communicate to all device by broadcasting. 
- It could communciate to a specific device by creating an id. 


When we are utilizing twi in a code, we need to include the `Wire.h` library