---
aliases: [De-multiplexer, demultiplexor]
---
# Demultiplexing
Demultiplex is the separation of information streams from the shared medium or multiplexed information
Demultiplexor is the device that perform demultiplexing

This transmit information from one [[Transmission Line]] to many devices, from serial data to parallel data.

And like [[Decoders]], it have an input line and an output line. The difference is that, it have 1 input line and it have additional lines called <u>select line</u>. Output line is dependent on the select line so if there are m select line, then the maximum number of output line is 2 ^ m or less (n <= 2^m)

![[Pasted image 20220927104426.png]]

The select line is important as this determines to which output line the input will be connected. 
So for we say we have 1 - 4 line demultiplexer with 2 select lines, the [[Truth Table]] is the following
![[Pasted image 20220927105001.png]]

Each output is still the [[Minterm]] of the select input such as y_0 is D because S_1'.S_0'.D == D. The following diagram for this is as follow
![[Pasted image 20220927105322.png]]

We use an [[NOT gate|Inverter]] again and 4 [[AND gate]] to pull this demultiplexor.
This are used in [[Components of Data Communication Network|Communication system]], computer chips, serial and parallel converters. 

# Metatags
###### Related: [[Multiplexing|Multiplexor]], [[Logic Gate]]
###### Tags: 
###### Source: 

---