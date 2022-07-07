---
aliases: [opcodes, ABI]
---
# Solidity
A programming language used to create [[Smart Contract]], its syntax is very similar to [[Javascript]] but hardtyped, meaning the [[Java Variables|data type]]s are defined in declaration,

Solidity transforms the source code into:
1. Opcodes or [[Etherum Virtual Machine|evm op code]]
2. ABI or applicaiton binary interface
3. Metadata

![[Pasted image 20220629162152.png]]

Bytecodes are the actual code converted from opcodes. 

Application binary interface looks like this;
![[Pasted image 20220629162257.png]]

Looks like an array with JSON file. 

Metadata on the other hand
![[Pasted image 20220629162410.png]]

Contains informaiton about our language, version, licence etc. 