---
aliases: [Y network]
---

# T Network
![[Pasted image 20220604092259.png]]

This is also called Y Network. Where 3 resistors collide in a Y or T formation

## Conversion
We can convert [[Pi network|Delta network]] to T network using this formula
![[Pasted image 20220604092822.png]]

$$R_1 = \frac{R_b R_c}{R_a + R_b + R_c}$$
$$R_2 = \frac{R_c R_a}{R_a + R_b + R_c}$$
$$R_3 = \frac{R_a R_b}{R_a + R_b + R_c}$$
<br>

<blockquote>"Each resistor in the Y network is the product of the resistors in the two adjacent Δ branches, divided by the sum of the three Δ resistors"</blockquote><hr>

Simply, to calculate the resistance of a resistor in Y network, we must get the product of the resistors in its side and divide it to the [[Equivalent Resistance|sum of all resistance]]

As far I could see, this formula is quite similar to computing [[Types of Electric Circuit|parallel]] resistance which is to multiply the 2 resistor and divide it by [[Equivalent Resistance]]

## Balanced Formula
If all resistor in the Delta Network have the same value then the formula will be
$$R_{Y} = \frac{R_{\Delta} R_{\Delta}}{R_{\Delta} + R_{\Delta} + R_{\Delta}}$$
$$R_{Y} = \frac{R_{\Delta}\space^2}{3R_{\Delta}}$$
$$R_{Y} = \frac{R_{\Delta}}{3}$$
