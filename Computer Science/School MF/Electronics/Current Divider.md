# What is Current Divider?
Is a [[Types of Electric Circuit|parallel]] circuit where current is divided to parallel paths.


![[Pasted image 20220603095530.png]]


In this diagram, we could see the [[Network Topology Branches|Nodes]] are in parallel to each other

## Mathematical Formula
To find the [[Electric Current|Current]] for each resistor, we can apply the formula of [[Ohm's Law]] 
$$i_1 = \frac{v}{R_1}$$
$$i_2 = \frac{v}{R_2}$$
Now, we can apply [[Kirchoff's Current Law|KCL]] here to go further $$i - i_1 - i_2 = 0$$
Substitute the components in our equation and we have $$i - \frac{v}{R_1} - \frac{v}{R_2} = 0$$
Reorganizing it and we get $$i = \frac{v}{R_1} + \frac{v}{R_2}$$
Simplify $$i = v\frac{1}{R_1} + \frac{1}{R_2} = v \big(R_{eq}\big)$$
Transpose $$v = i\big(R_{eq}\big)$$
[[Equivalent Resistance]] is equals to: 
$$\frac{1}{R_{eq}} = \frac{1}{R_1} + \frac{1}{R_2}$$
$$\frac{1}{R_{eq}} = \frac{R_2}{R_1R_2} + \frac{R_1}{R_1R_2}$$
$$\frac{1}{R_{eq}} = \frac{R_2 + R_1}{R_1R_2}$$
$$R_{eq} = \frac{R_1R_2}{R_1+R_2}$$
This formula is similar to the shortcut equation in [[Types of Electric Circuit]] parallel

Meaning, our equation is
$$v = i\frac{R_1R_2}{R_1+R_2}$$
Substitute it to the original equation and then we got
$$i_1 = i\frac{R_2}{R_1+R_2}$$
$$i_2 = i\frac{R_1}{R_1+R_2}$$
## Shortcut
To find the current in current divider, just use this method: $$i_n = i\frac{R_l}{R_1+R_2}$$
Where n is the nth current you are finding and $l \neq n$


