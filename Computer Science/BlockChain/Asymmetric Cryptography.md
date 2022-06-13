# What is Asymmetric Cryptography
This is also called as Public-key [[Cryptography]] that uses pair of keys namely
1. Public key
2. Private key


[[Public-key Generation|Generation]]s of this key pairs depends on the algorithm which is a one way function or something irreversible.

## Example
![[Pasted image 20220607045852.png]]

Bobs sends a messahe, the messahe was encrypted by the receiver's key, the encrypted message was sent and using the receiver's private key, she decrypts and done.

## Digital Signature
This example worls in reverse
![[Pasted image 20220607050057.png]]

Alice wants to send a message, she encrypt her message with her private key and sent both the original message and the encrypted to Bob, using Alice's public key, he decrypts it, if the message is equal to the encrypted message, then it will be received.
