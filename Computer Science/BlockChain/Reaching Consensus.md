# Reaching Consensus in Blockchain Transaction

This is one of the main problems of a blochain. How would they comfirm a transaction a transaction? How would they act to a disrepancy of information in a [[Blocks of Blockchain|block]] between nodes?

Not solving this problem will make the blockchain lose its purpose for a secure transaction.

To best represent it, read the [[Byzantine General Problem]]


## The Solution
Several famous blockchain network construct a consensus algorithm that solve this issue
such as [[Proof of Work Consensus Algorithm]]

#### Example:
For every transaction
- the database copy of a [[Blockchain Nodes|node]] is the same as any other [[Blockchain Nodes|node]], the *consensus is reached*
- the database copy of a [[Blockchain Nodes|node]] is not the same as any other [[Blockchain Nodes|node]], the *transaction is rejected*


