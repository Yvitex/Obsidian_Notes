---
aliases: [pulse width modulation, pwm]
---

# Analog Output Pins
Analog output pins are similar but different to a [[Digital Pins]]. They also could control the output of an output component such as [[LED]] but the difference is the intensity of the output. These pins are capable of [[Pulse Width Modulation]] and they are recognize using (~) tilde sign.
![[Drawing 2022-06-21 14.39.52.excalidraw.png]]

## Pulse Width Modulation
At this photo, we could see the [[voltage]] output is difference for each time. This is done through *PWM* or [[Pulse Width Modulation]] .

For an instance, a [[LED]] light was to be connected to an analog output. Using PWM, we set the output to be an alternating 5v and 0 very fast, the result will be evinced by light showing only half of its intensity.  In the other hand, analog output could also conceive a **True Analog Output**

## True Analog Output
In this way, we only set the [[Voltage]] output to be constant, what this means is that to half the intensity of an [[LED]] , we could just set the voltage output to the half of its value, for example is 2.5v.


## Example of PWM

![[Drawing 2022-06-21 14.53.18.excalidraw.png]]


| Analog Output # 11 | LED State      |
| ------------------ | -------------- |
| 0                  | Off            |
| 255                | On - Brightest |
| 50                 | On - Faint     |
| 200                | On - Bright    |
 
The value may range from 0 - 255 which is 0 when 8 bits of data is all 0, and 255 when all 8 bits of code is 1. Check [[Reading the Binary]] section, 