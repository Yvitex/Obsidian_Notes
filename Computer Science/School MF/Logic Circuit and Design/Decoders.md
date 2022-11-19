---
aliases: []
---
# Decoders
A Digital circuit thatd decodes [[Binary]] information in [[Digital System]]. Decoders have 2 basic parts which are <u>input line</u> and <u>output lines</u>. 

Input lines are where we feed our [[Binary]] data. Output line then represent the equivalent [[Minterm]], for any input, only one output line is activated at a time.
![[Pasted image 20220927100652.png]]

As we can see above, n number of input lines will have a maximum number of 2^n output lines. So for 3 input lines, we will have have a maximum of 8 output line but could have any lesser depending if some combinations are unused and we represent this output line as m. We could represent any decoder as n - m line decoder so in our case, it is a 3 - 8  line decoder. So m < 2^n. The number of input lines will also represent the the n -bit digital data, so if there is 3 input line, it means it could decode 3 bit digital data and could hadle m or 2 ^ n [[Binary]] symbol. 

```ad-Notice
title: Decoder vs Converter
collapse: open
Take note that in a decoder, output line is greater number than input line. If the output line and input line are equal, then they are called a converter.

```

These decoders mainly built using [[AND gate]] and [[NAND gate]] where [[AND gate]] is the basic decoding element. An example of this decoding is
![[Pasted image 20220927102046.png]]

Here we are decoding the [[Bit]] of 1001. This will be set to high because B and C use an [[NOT gate|Inverter]] to convert it into a High, meaning all of them is a High and with [[AND gate]], A.B.C.D == 1.

Another example is a 2 - 4 line decoder.![[Pasted image 20220927102851.png]]

Each output lines represent a [[Minterm]], for example D_0 is the result of A'B', D_3 is for AB. The resulting output could be as follow using a [[Truth Table]]
![[Pasted image 20220927103017.png]]

The digital diagram for this is 
![[Pasted image 20220927103041.png]]


Decoders are useful in [[Multiplexing|Demultiplexing]].
















# Metatags
###### Related: 
###### Tags: 
###### Source: 

---