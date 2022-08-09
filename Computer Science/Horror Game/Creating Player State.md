---
aliases: [player state]
---
# Player State
Are like game state but instead of storing the level's information, it stores the player information, Each individual player have their own player state, this is useful in storing health status, highscore etc.

Also, separating player state, [[Creating Game State|game state]] and [[Creating Game Modes|game mode]] are not important when it comes to a single player game so don't worry about details.

## Setup
The same process as in [[Creating Game State|game state]]. Withing the blurpring > curren level along with the [[Creating Game Modes|game mode]] and [[Creating Game State|game state]] bp, we create another blueprint called *PlayerState* then rename it to the current level + \_PlayerState
![[Pasted image 20220714055914.png]]

Inside the game mode, inside classes > Player State Class, change it to the created player state
![[Pasted image 20220714060020.png]]

Then compile.