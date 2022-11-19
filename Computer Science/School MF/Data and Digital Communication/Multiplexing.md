---
aliases: [Multiplexor, Data Selector]
---
# Multiplexing
This is the ability of device to share transmission facility

![[Pasted image 20220912111436.png]]

Multiplex is the combination of information streams from different devices so that it will be transmitted over the shared medium
Multiplexor is the device that performs multiplexing

Multiplex is from many to one meaning it converts parallel data to serial data also called as Data Selector. This is the same as [[Encoder]] except that it ave multiple input line but only a single output line with several number of select line controlling the input line.

The number of input line is dependend on the number of select line. If there is only 2 select line, then we could have a maximum of 2 input line. (n <= 2 ^ m)

![[Pasted image 20220927113343.png]]


To a 4 input line multiplexor, we have the following [[Truth Table]]
![[Pasted image 20220927113437.png]]

Like [[Encoder]], we use [[AND gate]], [[OR gate]], [[NOT gate]]
![[Pasted image 20220927113554.png]]

This are used in [[Data Communication]], computer memories, etc