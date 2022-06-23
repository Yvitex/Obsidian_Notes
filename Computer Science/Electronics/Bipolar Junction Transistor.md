---
aliases: [BJT, emitter, collector, base]
---

# What is BJT?
A 3 terminal transistor. It is called bipolar junction transistor because of the following reason
- It is bipolar or having 2 pairs of polarities
- It has a [[P-N Junction|junction]] that insulates the part. 

## Parts
1. Emitter - souce of [[Electric Charge|charge]] carriers
2. Collector  - collects [[Charge Carriers]]
3. Base - passage or path of [[charge carriers]]

## Types
1. [[NPN]] - emitts [[Electron Flow]] as emitter is highly [[Doping|doped]] with [[Atom is the smallest particle than an element can be reduced to|electron]]
2. [[PNP]] - emits [[Holes Flow]] as emitter is highly [[Doping|doped]] with [[Holes]]

![[Pasted image 20220603105103.png]]

But personally I call it sandwhich

![[Pasted image 20220603105148.png]]


- N = [[Doping|N-type semiconductor]] = \[majority carrier: [[Electrons]], minority carrier: holes]
- P = [[Doping|P-type semiconductor]] = \[majority carrier: [[Holes]], minority carrier: electron]


## Mathematical Formula
$$I_c = \beta I_b$$
where $$\beta = hfe$$
-  Ic = Collector Current
- Ib = Base Current
- Beta =  [[hfe]] 

## Symbols
![[Pasted image 20220611133147.png]]
Notice NPN pointed its arrow in emitter rather than to the [[Bipolar Junction Transistor|collector]]. It is because we are following the engineering convention where [[Electron Flow]] runs opposite to the [[Electric Current|Current]]. While [[Holes Flow]] runs the same as [[Electric Current|Current]]


We can use the [[Kirchoff's Current Law|kcl]] to create a new equation which is

![[Pasted image 20220603112619.png]]


The direction of the [[Electric Current|Current]] will always be from higher potential or [[Voltage]] to the [[Ground]] or negative voltage
By the way, PNP transistor looks like this ![[Pasted image 20220611140804.png]]


$$I_E = I_B + I_C$$
Substitute this to our first equation and we get
$$I_E = I_B + \beta I_B$$
Simplify
$$I_E = I_B \big( 1 + \beta\big)$$


Accordingly, if $\beta$ is greater than 100. Then the difference between $I_E$ and $I_C$ will be negligible, therefore $$I_E \approx I_C$$ 


