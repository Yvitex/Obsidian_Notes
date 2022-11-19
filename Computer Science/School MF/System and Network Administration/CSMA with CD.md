---
aliases: [CSMA/CD, Carrier Sense Multiple Access with Collision Detection]
---
# CSMA with CD
A technique that acts in a data collision
Let's break down its meaning:

<u>Carrier Sense</u> means it first tries to listen if a device is sending [[Packets]] over the network, if it does not detect anything, then it will assume that the [[Network]] is free and sends the data.

<u>Multiple Access</u> means their is no stopping the devices from sending [[Packets]] at the same time. 2 Devices might listen and once they determine that the network is free, they sent data at the same time which will cause a collision. 

<u>Collision Detectio</u>n means listening carefully when [[Packets]] crash to each other, when this occurs, it will be resent in different delay periods so that a second collision is unlikely.

This technique is only good for small networks, but for big ones like having 30 computers or nodes, data begins to collide like crazy so we usually divide it with compartment or sections called <u>Collision Domains</u>









# Metatags
###### Related: [[Data Layer]]
###### Tags: #networking 
###### Source: 

---