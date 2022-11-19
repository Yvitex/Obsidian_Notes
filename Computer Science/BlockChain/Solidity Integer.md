---
aliases: []
---
![[Pasted image 20221101122111.png]]

Are ordinary numbers that could range from 8 bits to 256 bits in size. All of its minimum is all 0s, and the max values are simply 2 to the power of their bits minus 1. Uint256 can be shorten to just uint and use this as a beginner for efficiency in speed because the smaller ones might be better in terms of storage but... they are still going to be converted to 256 bits in the end. 

We could also use negative numbers, just remove the u in the int as in unsigned. 
![[Pasted image 20221101122445.png]]

Now we have negative, the negative part could have a maximum number of 2 raise to the bitsize reduced by 1, then multiplied by negative 1. The maximum positive number is 2 raise to the power of its bitsize reduced by 1, then minus 1. 

# Metatags
###### Related: [[Solidity Language]]
###### Tags: 
###### Source: 

---