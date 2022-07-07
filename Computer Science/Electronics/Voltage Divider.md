# What is Voltage Divider?

A voltage divider is a simple [[Types of Electric Circuit|series]] circuit composed of 2 resistor and a [[2 Types of Electronic Sources|Source]]
![[Pasted image 20220603091921.png]]

## Mathematical Formula
To measure the [[voltage]] of individual [[Resistor|Resistor]]. We use the formula for [[Ohm's Law]]
$$v_1 = iR_1$$ $$v_2 = iR_2$$
Then we could use the [[Kirchoff's Voltage Law|KVL]] $$-v +v_1 + v_2 = 0$$
Substitute the equation and we have $$-v + iR_1 + iR_2 = 0$$
Modifying it $$v = i\big(R_1 + R_2\big)$$
Transpose $$i = \frac{v}{\big(R_1 + R_2\big)}$$
Substitute it to the first equation and we have $$v_1 = \frac{v}{\big(R_1 + R_2\big)}R_1$$ $$v_2 = \frac{v}{\big(R_1 + R_2\big)}R_2$$
Now we have the formula for voltage divider

Also $\big(R_1 + R_2\big)$ is also called [[Equivalent Resistance]] which basically means, sum of all resistance. The symbol for that is $R_{eq}$


## Shortcut
To find the voltage in a voltage divider, just use this method:
$$v_n = \frac{v}{\big(R_1 + R_2\big)}R_n$$
To find the voltage of n, we multiply the resistance of n with the quotient of total voltage with the equivalent resistance



