# Communication Protocol
A system of *rules* that allow 2 or more device to transmit information via some variations of physical quantity. 

## Types
- Text based - These are things that are made to be human readable. And example of this are, [[Common Ports|FTP]], SMTP etc.
- Binary - based on bits, 0 and 1 made to be computer readable but not to a human. 


## Arduino Specifics
There are several types of communication protocol existing in the [[The Arduino]] board. 

### UART LLT Serial Communication
UART means, Universal Asynchronous Receiver Transmitter
This exist along with [[Digital Pins]] 0 (RX) and 1 (TX). This 2 pins and their UART serial communication are responsible for the functionality of [[The Arduino]]'s  Atmel Atmega 16u connection to the USB, where then it will passed into the 328p. ![[Pasted image 20220621162740.png]]
Arduino uno only has a single UART interface, this are pin pairs. 
- TX = transmit data
- RX = receive data
Sometimes, it is necessary to have multiple UART interface, what we could do is to use other [[Digital Pins]] and emulate the same functionality through a software. 