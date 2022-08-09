---
aliases: [game instance]
---
# Game Instance
After [[Setup Level|setting up]], we could now create a game instance that will override the default ones. Game instance are like global variables useful in making health bars or mp barns that don't reset when the game progress or move to a different level, It is created when the game starts and deleted when the game is closed, somehow reminds me of [[Reference Type]] variables stored in [[Heap]]

## Setup
Create a new folder called BluePrint, or name it whatever just notice that this is where we will store blueprints. 
Create a new Blueprint class and search for game instance
![[Pasted image 20220714051541.png]]

rename it as horror game instance or whatever. Next is to set the default game isntance to that game instance. Go to settings > project setting > maps and modes > game instance. Then change it to horror game instance
![[Pasted image 20220714051749.png]]

