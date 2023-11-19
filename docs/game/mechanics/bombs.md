---
layout: default
title: Bombs
parent: Mechanics
grand_parent: Game
nav_order: 1
---

The game will feature different types of bombs that have different properties to spice up the gameplay.

## Blast Types

Blast Types define how the bomb explosion behaves.

| ID   | Name            | Behavior                                                                                                                                          |
|------|-----------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| 0x00 | Linear          | Classic Bomberman Blast, makes a horizontal and vertical line of fire with the bomb in the center.                                                |
| 0x01 | Rectangular     | Similar to the Dangerous Bomb from Bomberman LIVE. Blasts a huge rectangle of fire that can't be stopped by anything.                             |
| 0x02 | LinearPlasma    | The pattern is similar to Linear, but the Fire can spread further than one breakable Block in each direction.                                     |
| 0x03 | Directional     | The Bomb blast will go into the direction the player was facing when he placed the bomb. The fire will go twice as far as with other blast types. |
| 0x04 | LinearWide      | Same as Linear but each line is 3 Tiles wide.                                                                                                     |
| 0x05 | DirectionalWide | Same as Directional but the Blast is 3 Tiles wide.                                                                                                |
| 0x06 | PlasmaWide      | Same as LinearPlasma but the Blast is 3 Tiles wide.                                                                                               |
| 0x07 | Meshed          | Similar to a Linear blast, but it will split up at an intersection rather than stop.                                                              |

## Bomb Types
The types of available bombs are as follows

**If no sprite is present, it can be assumed that the bomb is not yet implemented.**
| Sprite                                  | Name             | Blast Type   | Long Ignition Time | Fast Ignition Time | Fire Radius | Fire Burn Time | Powerup ID |
|-----------------------------------------|------------------|--------------|--------------------|--------------------|-------------|----------------|------------|
| ![](/assets/img/mb/Bomb.png)            | Bomb             | Linear       | 3s                 | 2.5s               | 1           | 250ms          | None       |
| ![](/assets/img/mb/QuickBomb.png)       | Quick Bomb       | Linear       | 1.5s               | 1s                 | 1           | 150ms          | 0x000b     |
| ![](/assets/img/mb/StallBomb.png)       | Stall Bomb       | Linear       | 5s                 | 3s                 | 1           | 2000ms         | 0x000c     |
| ![](/assets/img/mb/MolotovCocktail.png) | Molotov Cocktail | Linear       | 2.0s               | 1.5s               | 1           | 750ms          | 0x0007     |
| ![](/assets/img/mb/NapalmBomb.png)      | Napalm Bomb      | LinearWide   | 3.5s               | 2.5s               | 1           | 1500ms         | 0x0008     |
| ![](/assets/img/mb/PlasmaBomb.png)      | Plasma Bomb      | LinearPlasma | 2s                 | 1.5s               | 2           | 250ms          | 0x000d     |
| ![](/assets/img/mb/Nuke.png)            | Nuke             | Rectangular  | 3.5s               | 2.5s               | 1           | 1750ms         | 0x000e     |
|                                         | Mesh Bomb        | Meshed       | 3.5s               | 2.5s               | 1           | 250ms          | N/I        |
|                                         | Focus Bomb       | Directional  | 3s                 | 2s                 | 2           | 250ms          | N/I        |
|                                         | RC Bomb*         | LinearWide   | N/A                | N/A                | 1           | 500ms          | N/I        |

*The RC Bomb will be detonated by a Player. Once the detonation is activated, the Bomb will explode after 300ms.