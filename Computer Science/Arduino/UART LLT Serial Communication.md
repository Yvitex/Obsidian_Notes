### UART LLT Serial Communication

UART means, *Universal Asynchronous Receiver Transmitter*

This exist along with [[Digital Pin]] 0 (RX) and 1 (TX). This 2 pins and their UART serial communication are responsible for the functionality of [[Arduino]]'s  Atmel Atmega 16u connection to the USB, where then it will passed into the 328p. ![[Pasted image 20220621162740.png]]
Arduino uno only has a single UART interface, this are pin pairs. 
- TX = transmit data
- RX = receive data
Sometimes, it is necessary to have multiple UART interface, what we could do is to use other [[Digital Pin]] and emulate the same functionality through a software. 