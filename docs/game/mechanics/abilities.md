---
layout: default
title: Abilities
parent: Mechanics
grand_parent: Game
nav_order: 1
---

An Ability grants an effect that can be activated on demand by the player. If multiple Ability Powerups are collected, the player can switch between the available abilities.

**If no sprite is present, it can be assumed that the ability is not yet implemented.**

| Sprite                                       | Ability        | Description                                                                                                                                                | Powerup ID |
|----------------------------------------------|----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| ![](/assets/img/mb/BombKickAbility.png)      | Bomb Kick      | Allows the player to walk up to a bomb and kick it in a straight line towards the next wall or player.                                                     | 0x0006     |
| ![](/assets/img/mb/InvincibilityAbility.png) | Invincibility  | Grants the player invincibility for X seconds. Timer configured in Game Type.                                                                              | 0x000f     |
| ![](/assets/img/mb/BombFreezeAbility.png)    | Bomb Freeze    | Freezes all Bomb timers for X seconds. Timer configured in Game Type.                                                                                      | 0x0010     |
|                                              | Bomb Rain      | Places all available Bombs in random walkable spots on the map.                                                                                            | N/I        |
|                                              | Gasoline Rain  | Replaces a certain percentage of floor tiles with gasoline spills randomly.                                                                                | N/I        |
|                                              | Earthquake     | All Bombs on the map will be moved in random directions.                                                                                                   | N/I        |
| ![](/assets/img/mb/PowerupRadarAbility.png)  | Powerup Radar  | Makes Powerups in nearby bricks visible for X seconds. Timer configured in Game Type.                                                                      | 0x0011     |
| ![](/assets/img/mb/LineBombAbility.png)      | Line Bomb      | Places a Line of Bombs in front of the player for as many bombs as the player can place at once. Line can be ended prematurely by Walls.                   | 0x0009     |
|                                              | Hyperspeed     | Temporarily increases Player Velocity by X pps for X seconds. Timer and boost configured in Game Type. This effect will ignore the configured speed limit. | N/I        |
|                                              | Bomb Pickup    | Allows the player to Pickup and throw a Bomb.                                                                                                              | N/I        |
|                                              | Fire Spit      | Spawns fire on the next two tiles directly in front of the player.                                                                                         | N/I        |
|                                              | Object Phasing | Allows the player to walk through most tiles that aren't solid walls for 15 seconds.                                                                       | N/I        |
|                                              | Wall Skip      | Allows the player to jump over a single Wall Tile to the next Walkable Tile.                                                                               | N/I        |
|                                              | Paint Trail    | Exclusive to Paint Bomb mode. Players will color any Tile they walk on for a configurable amount of seconds.                                               | N/I        |
|                                              | Chroma Shock   | Exclusive to Paint Bomb mode. Sends a Linear shockwave that can only hit opposing players. It will travel until it reaches a wall or a color border.       | N/I        |