---
aliases: [cipher, encrypt]
---
# Database Encryption
How can we encrypt [[Databases|database]]s in our application? HELL, what the heck is **encryption**?

## Encryption
It is a technique to hide information from bare sight, one of the earliest encryption thingy is called **Caesar Encytion**
![[Pasted image 20220613160913.png]]
How it works are just letters and key to decrypt it is a number which is the total amount of shifts from one letter to another. You can use this webiste called [cryptii](https://cryptii.com/pipes/caesar-cipher) to try it out. 

So, an encrypted text is also called a *Cipher Text*

Another one famous for decryption is the Enigma machine used by German's in world war 2. 
Currently, [[Public Ledger|Blockchain]]s are using those what we call [[Hashing Function]] to encrypt datas in a process called [[Cryptography]]

For database encryption in the other hand, we use AES-256-CBC encryption in [mongoose-encryption](https://www.npmjs.com/package/mongoose-encryption) for, of course, [[Mongoose Create Operations]] 

Now, how to use [[mongoose-encryption]] module. 


