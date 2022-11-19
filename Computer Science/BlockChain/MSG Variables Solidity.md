---
aliases: []
---
There are 4 variables that we could access using msg. And they are:
- msg.sender
- msg.value
- msg.data
- msg.sig

msg.sender contains the sender of the transaction. 
msg.value is the amount of token to be sent in wei
msg.data is not used because we could access it using function parameters
msg.sig is the 4 bits of code which is called Function Selector. 

But note that because it is only 4 bits, there are cases of data collision. Hackers do take advantage of this as with the Poly Bridge Attack which lost billion dollars which was returned by the hacker. 

# Metatags
###### Related: [[Solidity Language]]
###### Tags: 
###### Source: 

---