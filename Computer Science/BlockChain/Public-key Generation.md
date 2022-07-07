---
aliases: [address]
---

# How are they Generated?
- First thing is to generate a **private key** of a (64 hex characters)
![[Pasted image 20220607054958.png]]
- Second is to create a **public key** from the private key (128 hex characters)
- Next is to generate an **account address** from the public key (note that this is a 40 [[Hexadecimal Notation]] of just a portion of the public key and not the whole public key itself)![[Pasted image 20220607055058.png]]
- The number of hex is inexact. But it was derived from bytes or bits


Creating an address means generating both the [[Asymmetric Cryptography|private key]] and [[Asymmetric Cryptography|public key]]. The amount of randomly generate accounts is 256 bits meaning the amount of accounts that could be randomly generated is 2^ 256 more than the width of the universe. 
![[Pasted image 20220629042336.png]]
