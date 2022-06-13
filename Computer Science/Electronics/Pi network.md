---
aliases: [Delta network]
---


# Pi Network
![[Pasted image 20220604093300.png]]

Can be also called as Delta network, we can see that the figure above is one and the same because they are connected to the same [[Network Topology Branches|Node]]

## Conversion
To convert a [[T Network]] to delta network, we can use this formula:
![[Pasted image 20220604092822.png]]

$$R_a = \frac{R_1R_2 + R_2R_3 + R_3R_1}{R_1}$$
$$R_b = \frac{R_1R_2 + R_2R_3 + R_3R_1}{R_2}$$
$$R_c = \frac{R_1R_2 + R_2R_3 + R_3R_1}{R_3}$$
<br>
<blockquote>"Each resistor in the Δ network is the sum of all possible products of Y resistors taken two at a time, divided by the opposite Y resistor"</blockquote>
<hr>

To find the resistance in the delta network, we just need to find the sum of all possible product in the Y network and divide it by the opposite Y [[resistors|resistor]]

## Balanced Formula
If all resistor in the Y Network have the same value then the formula will be
$$R_{\Delta} = \frac{R_YR_Y + R_YR_Y + R_YR_Y}{R_Y}$$
$$R_{\Delta} = \frac{3R_Y \space^2}{R_Y}$$
$$R_{\Delta} = 3R_Y$$



