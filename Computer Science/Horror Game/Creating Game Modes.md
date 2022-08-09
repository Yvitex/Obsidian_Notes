---
aliases: [game mode]
---
## Game Modes
Unlike [[Creating Game Instance|game instance]] that is created when the game starts and deletes when they leave the game, game modes are created when the level starts and deleted when they exits the level.

Ever level needs a game modes as it acts as the storage of information of a certain level, in multiplayer games for instance is that they are the one responsible when player joins or leave the game and only the server have access to it.

## Setup
For every level, we need a game mode. To do this, inside our blueprint folder, create another folder called Level1 which will be the bp of our level1. Next is to create a new class and that class type will be the *game mode base*, rename it to Level_1_game_mode
![[Pasted image 20220714053132.png]]

To set the created game mode, go to setting and underthe game mode, select our created blueprint
![[Pasted image 20220714053221.png]]

Each level have their own game mode, if not, it will use the default game mode, we could set the default game mode into something. Go to setting > project setting > maps and mode > game mode
![[Pasted image 20220714053344.png]]

Game mode have also this subcategories which we will discuss in future lessons
![[Pasted image 20220714054401.png]]

They are the:
- [[Creating Game State|game state]]
- [[Creating Player State|player state]]
- [[Creating HUD Class|HUD Class]]
