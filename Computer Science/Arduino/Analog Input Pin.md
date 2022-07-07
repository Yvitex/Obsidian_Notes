# Analog Input Pins
Unlike [[Digital Pin]] that could only read values from 2 extremes, on and off, like [[Analog Output Pin]] they could read in in between values. 


![[Drawing 2022-06-21 15.25.08.excalidraw.png]]


For an instance we have an analog device called [[Potentiometer]], it have 3 pins, one is connected to analog pin # 0, another is connected to the [[Voltage Relationships in BJT|VCC]] and another in [[Ground]]. When the potentiometer is turned, it will change the voltage value from 0 - 5v and this is equivalent into the numerical value from 0 - 1023 inside hte analog input.

| Potentiometer Value | Voltage | Numerical Value |
| ------------------- | ------- | --------------- |
| 0                   | 0v      | 0               |
| 10                  | 5v      | 1023            |
| 5                   | 2.5v    | 511             |
| 2                   | 1v      |         204        |
