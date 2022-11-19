---
aliases: []
---
# Priority Encoder
This is a type of [[Encoder]] that assigns a priority. If 2 or more inputs are high, it will take the priority as the final reference.

In here if we have a 4 - 2 line priority encoder, D0 to D3, and D3 is the highest priority, the outputs are Y0 and Y1. If D3 is 1, the outputs are 11 regardless of other input, if D3 is 0 and D2 is 1, the output could be 1 0 regardless of other input.

![[Pasted image 20220927112152.png]]

We could see their is a range of important. When all inputs are low, the outputs is off??, Only ig the highest priority became High would the outputs become all High. If the secondart highest priority is High, the output is high, and so on. If the higher priority is high, it won't look at lower priorities. 

This could be constructed using [[AND gate]], [[OR gate]] or [[NOT gate]].
![[Pasted image 20220927112440.png]]









# Metatags
###### Related: [[Encoder]]
###### Tags: 
###### Source: 

---