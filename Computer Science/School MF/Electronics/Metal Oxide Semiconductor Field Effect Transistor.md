---
aliases: [MOSFET]
---
# MOSFET
Usually famous for their use in memory cards, well, it think that is Floating Gate MOSFET. But who cares, it's almost the same. Unlike, [[Junction Field Effect Transistor]], and [[Bipolar Junction Transistor]], this contains 4 terminals. 

## Terminals
- Source
- Drain
- Gate
- Body (Substrate(SS)) 

![[Pasted image 20220608120314.png]]


## Substrate
Unlike [[Junction Field Effect Transistor|JFET]], substrate's channel region works in reverse.
- If the substrate is a [[Doping|P-type semiconductor]] then it is a N-channel
- If the substrate is a [[Doping|N-type semiconductor]], then it is a P-channel

Substrate [[Present Perfect Continuous|has been]] separated with silicon dioxide which is an [[Insulator]]. The gate which a metallic plate will not touch the substrate



## When Attached to a Source
![[Pasted image 20220608144952.png]]

- $V_{DD}$  is the source. It is the difference between the drain voltage with respect to [[Ground]] or negative terminal of the source
- $V_{GS}$ is the voltage difference between the source and gate just like [[Junction Field Effect Transistor|JFET]]


## Modes
1. Depletion Mode - Already has a connection between source and drain, [[Conductance]] between source and drain $V_{DD} \downarrow$ decreases in relative to $V_{GS}$

The figure is oppositve of enchancement mode and works when it is on P-channel. We need to reverse the polarities of $V_{GS}$  so that negative voltage will repel electrons attracting bunch of holes for bridging. Refer to the enchancement mode.


2. Enchancement Mode - Have no connection between source and drain, conductance between source and drain $V_{DD} \uparrow$ increases relative to $V_{GS}$
![[Pasted image 20220612100149.png]]
In enchancement mode, the MOSFET is N Channel.  [[Electric Current|Current]] can flow when we apply a postive [[Voltage]] in $V_{GS}$
that causes an attraction to the [[Electrons]] creating bridge between source and drain. MEanwhile there is a negative voltage from the source $V_{DD}$  attracting bunch of [[Holes]] to the sides
Related: [[2 Types of Element in a Electronic Circuit|Active Element]]


## Schematics Types
![[Pasted image 20220612104706.png]]

![[Pasted image 20220908112512.png]]