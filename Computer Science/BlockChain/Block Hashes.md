# How does the Block Chains Works?

The [[Blocks of Blockchain|blocks]] in the [[BlockChain]] contains [[Cryptography|cryptographic]] hashes from some [[Hashing Function]] as their header. The next block in the chain have its own hashes, and also contains the hash of the previous hashes creating the chain of blocks.

In [[BlockChain Security]] we said that to tamper the system, we need a supercomputer that can overpower 51% of the computers. Because of the chaining system in the blockchain, to tamper a single transaction of the block, you need to modify the hashes of the entire history of the transaction as block 10 contains all information of block 9 and block 9 contains the information of block 8 and so on.

![[Pasted image 20220607045154.png]]

