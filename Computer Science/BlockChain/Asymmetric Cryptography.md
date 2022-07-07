---
aliases: [private key, public key]
---

# What is Asymmetric Cryptography
This is also called as Public-key [[Cryptography]] that uses pair of keys namely
1. Public key - encrypt data
2. Private key - decrypt data


[[Public-key Generation|Generation]]s of this key pairs depends on the algorithm which is a one way function or something irreversible.

## Example
![[Pasted image 20220607045852.png]]

Bobs sends a messahe, the messahe was encrypted by the receiver's key, the encrypted message was sent and using the receiver's private key, she decrypts and done.

## Digital Signature
This example worls in reverse
![[Pasted image 20220607050057.png]]

Alice wants to send a message, she encrypt her message with her private key and sent both the original message and the encrypted to Bob, using Alice's public key, he decrypts it, if the message is equal to the encrypted message, then it will be received.


## In Other Sources
The explanation provided above was slightly different, the user uses the public key to encrypt data and is signed by their private key. In actuality, the private key plus the data are the signature combined. They will publish the public key to the public and the public will veryify the transaction. No one can imitate your signature without your private key, 
