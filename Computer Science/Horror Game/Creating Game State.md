---
aliases: [game state]
---
# Game State
Is very similar to [[Creating Game Modes|game mode]] but the only difference is that in game state, it could nbe accessed by player and server, game mode, only the server. It stores level information such as the current goal, time etc.

## Setup
Inside the blurprint folder > Level. Create a new blurprint along with the [[Creating Game Modes|game mode]] blue print. Search for game state and select *GameStateBase*
![[Pasted image 20220714055010.png]]

Rename it to the current level + \_GameState
To use it, press the level's game mode and along with classes find game state class, use your game state bp
![[Pasted image 20220714055157.png]]
