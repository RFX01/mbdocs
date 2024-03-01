---
layout: default
title: Game Type Options
parent: Mechanics
grand_parent: Game
nav_order: 1
---
Powerup Sets
============

Powerup Sets are used for controlling Powerup Spawning (unless fixed Powerups are used). This set is a collection of different types of Powerups. Each Powerup will have a weight and limit associated with it. The weight defines the spawn chance of the Powerup. The limit determines the maximum amount of this type of powerup that should be spawned. These parameters are only used for procedural powerups and ignored for random Powerups, although random Powerups will still be limited to this selection. If all available Powerups should spawn in Random mode, all Powerups should be added to the set.

Game Type Settings
==================

Game Types will have the option to select a huge variety of settings to increase playstyle possibilites as much as possible. Matches can be initiated with a certain game type. It will be stored in a file to allow sharing together with a map. These settings are split into different categories, which will be represented as pages ingame. The user can set the following values to customize the gameplay:

**WIP NOTE:** Paint Bomb, Respawns and Goal Rush might conflict with each other. Although finding a way to combine scoring from several of these modes could make for some interesting gameplay variation.

One way to take care of this issue could be prioritizing the win condition of certain options if they are enabled.

Could be ordered like this: _Goal Rush (Goal Tile reached) > Paint Bomb (most Painted Tiles) > Respawns (Kill Count) > Default (Last man standing)_

Gameplay
--------


| Option Name                  | Description                                                                                                                                                                       | Example Values                              |
| ------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------- |
| Paint Bomb                   | Bomb Fires color tiles, the player with the most colored Tiles wins.                                                                                                              | True/False                                  |
| Goal Rush                    | The match will still go on if only a single player remains. If all players die the match will Tie, no matter the order of deaths. The only way to win is by reaching a Goal Tile. | True/False                                  |
| Respawns                     | Players can Respawn and get points for killing other players. The player with the most points after the match ends wins.                                                          | True/False                                  |
| Respawn Delay                | The amount of time in seconds a player has to wait for a respawn to occur.                                                                                                        | 5 sec                                       |
| Respawn Invincibility        | The amount of time in seconds a player will be invincible after respawning.                                                                                                       | 0.5 to 10.0 sec                             |
| Time Limit                   | How long the game lasts before sudden death begins or a tie is determined. Specified in minutes.                                                                                  | 0 to 10 min                                 |
| Fixed Spawns                 | Use fixed spawn points from map data instead of random spawns.                                                                                                                    | True/False                                  |
| Map Loop                     | If the player leaves the map on one side, they will reappear on the other side.                                                                                                   | True/False                                  |
| Health Bar                   | Use a health bar instead of dying in one hit.                                                                                                                                     | True/False                                  |
| Health Bar Size              | How many times a player can get hit before dying. Numeric value.                                                                                                                  | 2 to 6                                      |
| Post Hit Invincibility       | How long players will be invincible after getting Hit.                                                                                                                            | 0.2 to 3                                    |
| Bomb Collision               | Disabling this will allow players to walk through Bombs.                                                                                                                          | True/False                                  |
| Player Collision             | Disabling this will allow players to walk through other Players.                                                                                                                  | True/False                                  |
| Sudden Death                 | After the time limit runs out, Sudden Death slowly spawns fire on the map until the entire map is covered (or all players die).                                                   | True/False                                  |
| Sudden Death Pattern         | In which pattern the fire will spread during sudden death.                                                                                                                        | Outward Spiral, Inward Spiral, Linear, Wipe |
| Sudden Death Spread Interval | How many milliseconds need to elapse for the next fire to appear during sudden death.                                                                                             | 100                                         |

Powerups
--------


| Option Name                | Description                                                                                                                                                                                                                                                                                    | Example Values            |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------- |
| Powerup Placement          | How powerups are spawned. Random places them randomly in any breakable blocks depending on the Random Powerup concentration and selection. Fixed will use fixed powerup positions and types from map data.                                                                                     | Random, Procedural, Fixed |
| Powerup Set                | Which powerups will be spawned. The weights and limits of the Powerup Set will be ignored if Random Powerups is enabled.                                                                                                                                                                       | (PowerupSet)              |
| Powerup Concentration      | How many percent of breakable Tiles will contain powerups. Only used for Procedural and Random Powerups.                                                                                                                                                                                       | 35%                       |
| Open Powerups              | Powerups can spawn openly on the map. Disabling this will prevent Fixed Open Powerups from spawning.                                                                                                                                                                                           | True/False                |
| Open Powerup Set           | Another Powerup Set used for Open Powerups.                                                                                                                                                                                                                                                    | (PowerupSet)              |
| Open Powerup Concentration | How many percent of walkable Tiles will contain open powerups. Only used for Procedural and Random Powerups.                                                                                                                                                                                   | 10%                       |
| Powerup Rain               | Powerups will be spawned on random Walkable tiles while the game is playing                                                                                                                                                                                                                    | True/False                |
| Powerup Rain Interval      | How many seconds need to elapse before the next Powerup Rain is triggered.                                                                                                                                                                                                                     | 1 to 120 seconds          |
| Powerup Rain Set           | Another Powerup Set used for Powerup Rain.                                                                                                                                                                                                                                                     | (PowerupSet)              |
| Powerup Rain Concentration | How many percent of walkable Tiles will have Powerups appear on them when a Powerup Rain is triggered.                                                                                                                                                                                         | 5%                        |
| Keep Keys                  | Keys can be reused an inifinite amount of times.                                                                                                                                                                                                                                               | True/False                |
| Collect Useless Powerups   | When enabled, Powerups can be collected regardless of whether or not they will change anything for the player picking them up. Disabling this would for example prevent a player with full health from collecting health powerups, a player at full speed from collecting speed ups and so on. | True/False                |
| Fireproof Powerups         | Fire will not destroy Powerups.                                                                                                                                                                                                                                                                | True/False                |

Bombs
-----


| Option Name               | Description                                                                                                                    | Example Values |
| --------------------------- | -------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| Bomb Switch               | Players can carry several different bomb types and switch between them at any time.                                            | True/False     |
| Limited Bombs             | Bombs can run out. Breaking blocks without a powerup inside them will drop a bomb that can be picked up by players to restock. | True/False     |
| Initial Limited Bombs     | How many bombs a player starts with when playing with Limited Bombs.                                                           | 10             |
| Fixed Bomb Sets           | Start players with a selection of bombs they chose beforehand.                                                                 | True/False     |
| Hidden Bombs              | Breakable blocks can have bombs hidden inside of them that explode once the block is broken.                                   | True/False     |
| Hidden Bomb Concentration | How many percent of breakable Tiles will contain Hidden Bombs.                                                                 | 10%            |
| Hidden Bomb Selection     | Which bomb types the hidden bombs can have.                                                                                    | DefaultBomb    |
| Hidden Bomb Min Radius    | The minimum Blast Radius hidden bombs will have.                                                                               | 1              |
| Hidden Bomb Max Radius    | The maximum Blast Radius hidden bombs will have.                                                                               | 3              |
| Initial Max Bombs         | Amount of bombs that can be placed at once initially. Defaults to 1.                                                           | 2              |
| Initial Bomb Selection    | Which bomb the players start with.                                                                                             | DefaultBomb    |

Abilities
---------


| Option Name               | Description                                                                                                                                                         | Example Values      |
| --------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------- |
| Infinite Abilities        | On-demand abilities can be used infinitely after being collected once.                                                                                              | True/False          |
| Ability Cooldown          | Make players wait for a cooldown to expire before being able to use the Ability again.                                                                              | True/False          |
| Initial Ability Selection | Which abilities should be given to the players once the match starts. Can also contain an amount of uses for the abilities for when Infinite Abilities is disabled. | List&lt;Ability&gt; |
| Invincibility Timer       | Controls how long Invincibility lasts in seconds once the corresponding Ability is used.                                                                            | 10                  |
| Bomb Freeze Timer         | Controls how long Bomb Timers are frozen in seconds once Bomb Freeze is used.                                                                                       | 5                   |
| Powerup Radar Timer       | Controls how long Powerup Radar will remain active in seconds once used.                                                                                            | 15                  |
| Powerup Radar Radius      | Set the radius in which powerups will be displayed (in tiles). More distant powerups will be less opaque.                                                           | 10                  |
| Object Phasing Timer      | Controls the duration of Object Phasing in seconds once the ability is activated.                                                                                   | 10                  |

Ability Cooldowns
-----------------


| Option Name             | Description                                | Example Values     |
| ------------------------- | -------------------------------------------- | -------------------- |
| Bomb Kick Cooldown      | Cooldown timer for Bomb Kick ability.      | 0.5 to 120 seconds |
| Line Bomb Cooldown      | Cooldown timer for Line Bomb ability.      | 0.5 to 120 seconds |
| Invincibility Cooldown  | Cooldown timer for Invincibility Ability.  | 0.5 to 120 seconds |
| Bomb Freeze Cooldown    | Cooldown timer for Bomb Freeze ability.    | 0.5 to 120 seconds |
| Powerup Radar Cooldown  | Cooldown timer for Powerup Radar ability.  | 0.5 to 120 seconds |
| Object Phasing Cooldown | Cooldown timer for Object Phasing ability. | 0.5 to 120 seconds |
| Bomb Rain Cooldown      | Cooldown timer for Bomb Rain ability.      | 0.5 to 120 seconds |
| Gasoline Rain Cooldown  | Cooldown timer for Gasoline Rain ability.  | 0.5 to 120 seconds |
| Earthquake Cooldown     | Cooldown timer for Earthquake ability.     | 0.5 to 120 seconds |
| Flamethrower Cooldown   | Cooldown timer for Fire Spit ability.      | 0.5 to 120 seconds |
| Bomb Pickup Cooldown    | Cooldown timer for Bomb Pickup ability.    | 0.5 to 120 seconds |

Multipliers
-----------


| Option Name                  | Description                                                                                        | Example Values |
| ------------------------------ | ---------------------------------------------------------------------------------------------------- | ---------------- |
| Base Speed Multiplier        | Multiplies the base player velocity by the given factor.                                           | 1.5x           |
| Bomb Speed Multiplier        | Multiplies the velocity of moving bombs by the given factor.                                       | 1.5x           |
| Base Fire Radius Multiplier  | Multiplies the base fire radius of a bomb by the given factor.                                     | 2x             |
| Base Burn Time Multiplier    | Multiplies the base burn time of a bomb by the given factor.                                       | 1.5x           |
| Fire Up Multiplier           | Multiplies the Fire Radius increase from collecting Fire Ups by the given factor                   | 2x             |
| Bomb Up Multiplier           | Multiplies the MaxBombs increase from collecting Bomb Ups by the given factor.                     | 2x             |
| Speed Up Multiplier          | Multiplies the velocity increase from collecting Speed Ups by the given factor.                    | 1.5x           |
| Burn Time Up Multiplier      | Multiplies the Burn Time increase from collecting Burn Time Ups by the given factor.               | 1.5x           |
| Ignition Speed Up Multiplier | Multiplies the Fast Ignition Time decrease from collecting Ignition Speed Ups by the given factor. | 1.5x           |
| Ability Pickup Multiplier    | Multiplies the amount of uses gained when picking up abilities by the given factor.                | 2x             |
| Capsule Radius Multiplier    | Multiplies the spill radius of exploded capsules by the given factor.                              | 2x             |
| Map Timer Divider            | Divides the Values of all Time Bombs and Time Doors by the given divisor.                          | /1.5           |
| Fast Ignition Divider        | Divides the Fast Ignition timer by the given divisor.                                              | /1.5           |
| Long Ignition Divider        | Divides the Long Ignition timer by the given divisor.                                              | /1.5           |

Limiters
--------


| Option Name          | Description                                                                                                  | Example Values |
| ---------------------- | -------------------------------------------------------------------------------------------------------------- | ---------------- |
| Speed Limit          | Limits the player Velocity to the given amount.                                                              | 300            |
| Burn Time Limit      | Limits the Burn Time of Fires to the given amount of milliseconds.                                           | 3000           |
| Fast Ignition Limit  | Limits the fast Ignition timer to never go lower than the specified amount of milliseconds.                  | 500            |
| Fire Radius Limit    | Limits the Fire Radius of bombs placed by players. Set to 0 for no limit.                                    | 7              |
| Bomb Count Limit     | Limits the total amount of bombs by a player that can be on the map at the same time. Set to 0 for no limit. | 5              |
| Ability Pickup Limit | Limits the total amount of ability uses a player can have per ability. Set to 0 for no limit.                | 10             |
