---
aliases: [JFET]
---

# Junction Field Effect Transistor
Also called junction-gate field effect transistor

## Construct
![[Pasted image 20220608110735.png]]

### Parts
- Drain
- Gate
- Source
- Substrate

### Substrate
Substrate is the base of the material
- N-channel - composed of n type material filled with [[Electrons]] 
![[Pasted image 20220608110735.png]]
- P-channel - composef of p type material filled with [[Holes]]
![[Pasted image 20220608111349.png]]


- Difference of voltage between gate ans source - $V_{GS}$
- Difference of voltage between drain and source - $V_{DS}$

## How does it works in an N Channel?
- The [[Electron Flow|current flows]] from Drain to Source through [[Voltage]] applied in the gate
- We can see the figure above, there are 2  [[P-N Junction]] so there is also 2 depletion region with [[Insulator|insulation properties]], increasing the [[Voltage]] at the gate will expand the depletion region. Also it is also affected by the strength of $V_{DS}$
- The PN junction acts like a host that when restrict the space where [[Electron Flow|electron]] could flow, the [[Electric Current|Current]] will move faster So therefore, 
-  When $V_{DS}$ increase, $I_D$ also increase. 
![[Pasted image 20220612060337.png]]


Although this is the case, it is important to note about [[Pinch-off Voltage]]. It is the point where event if we increase $V_{DS}$, $I_D$ will not as the depletion region already blocks the path where electron could flow.

This is how it will look like with battery attached

![[Pasted image 20220608114135.png]]

- $V_{DD}$ is the source
## Schematic Symbols
1. P channel: Current goes out![[Pasted image 20220608114250.png]]
2. N channel: current goes in![[Pasted image 20220608114306.png]]

![[Pasted image 20220612051851.png]]
