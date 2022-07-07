# How to use Multimeter?

## To measure voltage
Remember the basics in measuring the [[Voltage]] in [[Voltage Relationships in BJT]]. To calculate the voltage supply is we substract the high potential to the ground which means $$V_{CC} - 0 = V_{CC}$$
First is we need to guess how much of a voltage it is, and we already know that the voltage source applicable to the power supply is configured to 5v. 

Red pin is for the positive and black for the negative...

![[Pasted image 20220625121052.png]]

Voltage drop is calculated by doing the same stuff but on a specific component.

## To measure Current
Here, we modify the circuit just a little bit. 
![[Pasted image 20220625145457.png]]

Here we form an open circuit... The [[LED]] in not turned on because it is a broken circuit. But never worry, the multimeter pins wil complete the transfer of [[Electricity]] by doing this
![[Pasted image 20220625145842.png]]

2 birds with one stone. We are currently measuring the [[Electric Current|Current]] while [[2 Extreme Scenarios of a Circuit|closing]] the circuit . Here reads that the led is currently accepting 3.049 mA of current. 

```ad-Attention
collapse: open
Before using the multimeter, we must first make our initial guess then configure the range of multimeter.

```

We could make our initial guess by calculation through the holy [[Ohm's Law]]

## To measure Resistance
It is very different from the previous measurement, as we don't need the components to be on a circuit at all. So we remove it from the current, set the multimeter to the predicted range value in [[Resistance]] ohn, and here, the polarity does not matter so you could put the 2 pins on either side of the component. ![[Pasted image 20220625153546.png]]

## Continuity Testing
![[Pasted image 20220625153720.png]]

We first set the multimeter to a continuity mode which is a wifi signal like symbol. Measuring this does not need to be powered up by a voltage source. Mind the polarity, red is for positive and black is for negative
![[Pasted image 20220625153927.png]]
When there is continuity, the multimeter will beep. 

![[Pasted image 20220625154122.png]]
If there is a resistance, the multimeter won't beep. [[LED]] has resistance, therefore it won't beep. 

