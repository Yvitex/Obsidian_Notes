# Digital Pins
Digital pins have 2 main functionalities:
- As a Digital Output
- As a Digital Input

Digital means, represented as a digit. And in the topic of arduino, the [[Microcontroller]] was able to recognize only 2 digits, and it is on [[Binary]] 

### Digital Representation
| Digit | Representation | Voltage Equivalence |
| ----- | -------------- | ------------------- |
| 0     | Low            | 0 - 3.0v            |
| 1     | High           | 3.5 - 5v                    |

## As Digital Output
Pins could change the state of an electrical component.

![[Drawing 2022-06-21 10.20.33_0.excalidraw.png]]

Suppose, we have a circuit that has an [[LED]] conencted from digital pin # 7 to the [[Ground]] (GND). If digital pin # 7 has a [[Voltage]] greater than 3v, then the led will turn on. If not or lower, then the LED wll turn off, it is a simple [[Switching Operation]] 


## As a Digital Input
Example of this is that, the same pins could read the state of a button. ![[Drawing 2022-06-21 11.18.20.excalidraw.png]]

Here, we connected the digital pin # 5 with a button to the [[Ground]]. But this is ignorance, we are leaving the digital pin to read the air rather than the [[Voltage]] when it is not pressed. This phenomenon is called [[Hanging Value]]. To fix this, we wil apply a [[Pull Up or Down Resistor]], guess if the circuit below is a pull up or pull down resistor
![[Drawing 2022-06-21 11.18.20.excalidraw 1.png]]

So here, when we are not pressing the button, the digital pin # 5 detects a high value of 5v, but when it is pressed, because the inclination of [[Electric Current|Current]] was to go to a path with less [[Resistance]], it will detect instead a Low value of [[Voltage]]




Answer: It is a Pull Up resistor as it is connected to the [[Voltage Relationships in BJT|VCC]] or source voltage of you know what i mean