# Analyzing Circuits
![[Pasted image 20220611150409.png]]

This diagram aboce shows a fixed bias. Or some [[Bipolar Junction Transistor|BJT]] circuit without emitter resistor in contrast to [[Emitter bias]], In this, $I_C$ is highlt dependent on the base. 


Remember that $V_{BE}$  is equals to 0.6 - 0.7, $R_B$ must be large aroung 100K ohms. Base does not need too much voltage nor current because it will break. The same is true to  [[LED]]

If it is an [[2 Extreme Scenarios of a Circuit|Open Circuit]], then no voltage will be applied to the base which means the base won't allow the [[Electric Current|Current]] from the [[Bipolar Junction Transistor|collector]] to flow to the emitter. The [[LED]] won't light up. 

$V_{BE}$  is the measure of voltage between $V_B$  and $V_E$ .

Noticing this, we could derive a formula that will solve $I_{B}$l

$$V_{BE} = V_B - V_E $$
$V_E$  is 0, therefore: $$V_{BE} = V_B$$
And $$V_{BE} \approx 0.6$$
So $$V_B = 0.6$$
According to [[Ohm's Law]]: $$i = \frac{v}{R}$$
So using this info...$$I_B = \frac{V_B}{R_B}$$
But I am wrong because we need to subtract the source to the $V_B$ to get the actual voltage drop, so the real equation is $$I_B = \frac{ V_{CC} - V_B}{R_B}$$
$$I_B = \frac{ V_{CC} - 0.6}{R_B}$$



 
