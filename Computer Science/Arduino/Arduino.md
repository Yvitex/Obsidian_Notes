# Arduino
![[Pasted image 20220621042733.png]]

Genuino and Arduino ar practically the same aside from their brand. The brain of the arduino uno is a [[Microcontroller]] called
**Atmel ATmega**, Take note that a microcontroller is different from [[Microprocessor]] and cpu. It has a lot of digital input and output pin allowing the microconroller to interact to the world around it and also it cannot run a program or any digital things. Microcontroller does not run an OS. 

## Atmel ATmega 328p
![[Pasted image 20220621043208.png]]

This could be removed using a flat screqdriver. Reattaching it. make sure to match the endpoint shape of the microcontroller to its container. ![[Pasted image 20220621043620.png]]
## Atmel ATmea 16u
![[Pasted image 20220621043742.png]]
This microcontroller is used specigically to control the communication between the USB and the brain or the Atmel ATmega 328p

## Headers
![[Pasted image 20220621044649.png]]
Black sockets are called **Long and Short Header**, because one of them is long and another is short. We could connect components through it using [[Jumper Wires]] Specifically male to male. (Note: Not Yaoi) 

## Shield
![[Pasted image 20220621044927.png]]

A component that could be attached to the arduino uno, by plugging it to the header expanding more of its capabilities and more such as ethernet connection or screen.

(Note: When attaching and disattaching shields, it is important to note that we need not to bend the pins or else it will break.)

## Types of Pins
Pins in the header have different functions, the 3 main groupd so of pins are resonsible for Power pins, [[Analog Input Pin]] and [[Digital Pin]] along with [[Analog Output Pin]].
![[Pasted image 20220621050839.png]]
![[Pasted image 20220621050917.png]]

SCL, SDA, AREF, 0 (RX), 1 (TX) are communication pins. Used to communicate extenal divice, such as sensor or other arduino,. SCL and SDA are used for popular [[Communication Protocol]] while RX and TX are for classic serial [[Communication Protocol]]

## Bottle Connector
Aside from the USB connected to the computer, we could power the arduino using socket through the bottle connector
![[Pasted image 20220621052016.png]]
(Note; the recommened [[Voltage]] supply it could take is 7 - 12 v. But it could exceed it to 6-20v which is the absolute limit. This is possible through the voltage regulator wchih is the black rectangle with 3 solver pins beside thr bottle connector. If exceeds pass to 9v, then it will start to generate a lot of wasted electricity in the form of heat that may brak the arduino )![[Pasted image 20220621052312.png]]

## ICSP
*In circuit serial programming*. Another way of prorgramming the arduino directly through the Atmel ATmega 328p and 16u.
![[Pasted image 20220621052606.png]]

## Reset Button
![[Pasted image 20220621052805.png]]

Reset the board. Execute the line of codes from the beginning. 

## Crystal Clock
Beats 6million times per second, this made the whole arduino board ticks that will run the codes. If broken, this won't run as if the time has stopped. [[Microprocessor]] also have this. 
![[Pasted image 20220621052904.png]]

## Capacitors
[[capacitor]] filters our the voltage to be steady. This functionality is also used in [[rectifier]] that makes triangular voltage graph to become perfect sinusoidal. 
![[Pasted image 20220621053117.png]]