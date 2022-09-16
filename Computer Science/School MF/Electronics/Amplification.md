---
aliases: [midpoint bias]
---
# BJT Amplification
To get the maximum amplification, we need to consider the  **MidPoint Bias**

## Midpoint Bias
Here is the formula for midpoint bias:
$$V_{CE} = \frac{1}{2}V_{CC}$$
Alternatively: $$I_C = \frac{1}{2}I_S$$

![[Pasted image 20220611150409.png]]

The [[Fixed Bias]] above is the diagram. The thing that will determine the maximum benefit is if the half of [[Voltage Relationships in BJT|voltage source]] is equal to the difference of [[Bipolar Junction Transistor|collector voltage]] and emitter voltage

$V_{CE}$  in this Diagram is: $$V_{CE} = V_C - V_E$$
$V_E = 0$  so: $$V_{CE} = V_C$$
Then the value of V_C is: 

$$V_{C} = V_{CC} - V_{RC} - V_D$$

$$V_{RC} = I_C R_C$$

Therefore: 
$$V_{CE} = V_{CC} - I_C R_C - V_D$$
