---
layout: default
title: Powerups
parent: Mechanics
grand_parent: Game
nav_order: 1
---

MadBomber will feature various Powerups. Some of them will be direct clones of Bomberman LIVE Powerups, some will be original.

**If no sprite is present, it can be assumed that the powerup is not yet implemented (with the exception of BombTypePowerup and AbilityPowerup).**

Basic Powerups
--------------

These are part of the standard powerups that can be spawned into any game. They upgrade basic player properties and give the player different bombs.

| Sprite                                      | Powerup             | Description                                                                                                            | Powerup ID                                           |
|---------------------------------------------|---------------------|------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------|
| ![](/assets/img/mb/BombUpPowerup.png)       | BombPowerup         | Increases the amount of bombs that can be placed at the same time by 1.                                                | 0x0001                                               |
| ![](/assets/img/mb/FireUpPowerup.png)       | FirePowerup         | Increases the radius of the bomb blast by 1.                                                                           | 0x0002                                               |
| ![](/assets/img/mb/BurnTimeUpPowerup.png)   | BurnTimePowerup     | Increases the amount of time the fire stays on the map by 50 milliseconds.                                             | 0x0003                                               |
| N/A                                         | BombTypePowerup     | Gives the player an additional Bomb Type or replaces the current Bomb Type. Will be viewed as many different Powerups. | See [Bombs](/docs/game/mechanics/bombs.html)         |
| N/A                                         | AbilityPowerup      | Gives the player an ability. Will be viewed as many different Powerups.                                                | See [Abilities](/docs/game/mechanics/abilities.html) |
| ![](/assets/img/mb/FastIgnitionPowerup.png) | FastIgnitionPowerup | Decreases the FastIgnitionTime of a Bomb by 0.1 seconds.                                                               | 0x0004                                               |
| ![](/assets/img/mb/SpeedUpPowerup.png)      | VelocityPowerup     | Increases the players Velocity. Experimentation is still needed to determine by how much.                              | 0x0005                                               |

Special Powerups
----------------

These powerups should only be spawned in certain game types.

| Sprite                                | Powerup            | Description                                                                  | Powerup ID |
|---------------------------------------|--------------------|------------------------------------------------------------------------------|------------|
| ![](/assets/img/mb/KeyPowerup.png)    | KeyPowerup         | Grants the player a key which can be used for unlocking a LockedDoor Tile.   | 0x000a     |
|                                       | LimitedBombPowerup | If playing with Limited Bombs enabled, grants the player an additional Bomb. | N/I        |
| ![](/assets/img/mb/HealthPowerup.png) | HealthPowerup      | If playing with a health bar, grants the player an additional Hit Point.     | 0x0012     |