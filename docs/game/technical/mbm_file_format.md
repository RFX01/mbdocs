---
layout: default
title: MBM File Format
parent: Technical
grand_parent: Game
nav_order: 1
---

Maps are stored in a binary file format called MBM (MadBomber Map). It consists of a header describing the map and a payload containing the tiles.

Header
======

The header has a total size of 7 bytes. The first 4 bytes will always describe the mbm Version, no matter which version the file is in.

| Header Byte Position | Description                                        | Example Content |
|----------------------|----------------------------------------------------|-----------------|
| 0x00 - 0x02          | Header start block. Always set to mbm.             | 0x4d424d        |
| 0x03                 | File Format Version. This document describes mbm1. | 0x01            |
| 0x04                 | Map Size X Byte                                    | 0x10            |
| 0x05                 | Map Size Y Byte                                    | 0x10            |
| 0x06                 | Spawn Count                                        | 0x02            |
| 0x07, 0x08           | Powerup Count, 16-bit                              | 0x001f          |
| 0x09                 | Teleporter Count                                   | 0x02            |
| 0x0a, 0x0b           | Time Bomb Count, 16-bit                            | 0x0001          |
| 0x0c, 0x0d           | Key Count, 16-bit                                  | 0x0001          |
| 0x0e                 | Author Name Length                                 | 0x0f            |
| 0x0f                 | Game Type Link Length                              | 0x0d            |
| 0x10, 0x11           | MapScript Trigger Count, 16-bit                    | 0x000a          |
| 0x12, 0x13           | MapScript Global Command Count, 16-bit             | 0x000d          |
| 0x14, 0x15           | MapScript User Variable Count, 16-bit              | 0x0003          |

### Example Header
```hex
4d 42 4d 01 10 10 02 00 1f 02 00 01 00 01 0f 0d 00 0a 0d 00 03
```

Payload
=======

Spawn Block
-----------

The Spawn Block has 2 bytes for each spawn point. The high byte containing the X coordinate, and the low byte containing the Y coordinate. The order these are saved in correspond to the spawn point for Player 1, then Player 2, and so on.

### Example Spawn Block
```hex
0d 0d 04 04
```

This example Spawn Block describes spawn points for 2 players. The first player will spawn in the top right corner, 1 tile away from the map border. The second player will spawn on the tile south to the first player.

Tile Block
----------

The Tile Block consists of a single byte for each Tile. This byte corresponds to the type of tile. The first X bytes of the payload correspond to the first row of tiles, the second X bytes of the payload correspond to the second row of tiles, and so on. The Tile Block size will be variable depending on the Map Size. See  for a list of IDs.

Powerup Block
-------------

The Powerup Block consists of 4 bytes for each Powerup. The bytes are structured as follows:

| Byte       | Content                                                               |
|------------|-----------------------------------------------------------------------|
| 0x00, 0x01 | Powerup type, see  for exact IDs. 0x0000 represents a random powerup. |
| 0x02       | X Position                                                            |
| 0x03       | Y Position                                                            |

Teleporter Block
----------------

The Teleporter Block consists of 4 bytes for each Teleporter. This Block stores Teleporter positions and their links. The bytes are structured as follows:

| Byte | Content                          |
|------|----------------------------------|
| 0x00 | The ID of the target teleporter. |
| 0x01 | X Position                       |
| 0x02 | Y Position                       |

Time Bomb Block
---------------

The Time Bomb Block consists of 4 bytes for each time Bomb. The stored values are the timer and the position in the following structure:

| Byte       | Content            |
|------------|--------------------|
| 0x00, 0x01 | 16-bit Timer Value |
| 0x02       | X Position         |
| 0x03       | Y Position         |

Key Block
---------

The Time Bomb Block consists of 4 bytes for each Key (Powerup or Lock). Contains KeyID and position in the following structure:

| Byte  | Content    |
|-------|------------|
| 0x00, | KeyID      |
| 0x01  | X Position |
| 0x02  | Y Position |

Map Author
----------

Just before the Game Type Link, the name of the map author will also be stored in plain text. This is simply for the purpose of knowing who made a specific map.

Game Type Link
--------------

At the very end of the file can be the name of a gametype if one is linked. This will simply be plain text. Used for associating a game type with a map.

MapScript Block
===============

The MapScript Block consists of three Parts, the Trigger Section, the Command Section and the Variable Section.

Trigger Section
---------------

A Trigger Section item begins with a single byte describing the Trigger Type. This determines how the following bytes will be structured.

| ID   | Trigger Type | Data Structure            |                      |                                        |                               |                                      |                                      |                     |                               |                                      |
|------|--------------|---------------------------|----------------------|----------------------------------------|-------------------------------|--------------------------------------|--------------------------------------|---------------------|-------------------------------|--------------------------------------|
| 0x00 | TimeTrigger  | Name Length  <br>**byte** | Name  <br>**string** | Trigger Time  <br>**float**            | Command Count  <br>**ushort** | Commands  <br>**Command Subsection** |                                      |                     |                               |                                      |
| 0x01 | MapTrigger   | Name Length  <br>**byte** | Name  <br>**string** | Condition  <br>**MapTriggerCondition** | TileX  <br>**byte**           | TileY  <br>**byte**                  | AreaX  <br>**byte**                  | AreaY  <br>**byte** | Command Count  <br>**ushort** | Commands  <br>**Command Subsection** |
| 0x02 | LoopTrigger  | Name Length  <br>**byte** | Name  <br>**string** | Trigger Time  <br>**float**            | Loop Delay  <br>**float**     | Command Count  <br>**ushort**        | Commands  <br>**Command Subsection** |                     |                               |                                      |

Command Section
---------------

This section will appear multiple times. Every trigger will have a Command Subsection. Another Command Section will appear right after the Trigger Section, defining the Global Commands.

A Command Section begins with a single byte describing the Command Type. This determines how the following bytes will be structured.

| ID   | Command Type         | Data Structure            |                      |                                    |                                     |                                |                              |                                     |                                |                                     |                                     |                                |                           |                            |                       |
|------|----------------------|---------------------------|----------------------|------------------------------------|-------------------------------------|--------------------------------|------------------------------|-------------------------------------|--------------------------------|-------------------------------------|-------------------------------------|--------------------------------|---------------------------|----------------------------|-----------------------|
| 0x00 | ReplaceTile          | Name Length  <br>**byte** | Name  <br>**string** | Tile X Length  <br>**byte**        | Tile X  <br>**string**              | Tile Y Length  <br>**byte**    | Tile Y  <br>**string**       | Tile ID Length  <br>**byte**        | Tile ID  <br>**string**        |                                     |                                     |                                |                           |                            |                       |
| 0x01 | SpawnPowerup         | Name Length  <br>**byte** | Name  <br>**string** | Tile X Length  <br>**byte**        | Tile X  <br>**string**              | Tile Y Length  <br>**byte**    | Tile Y  <br>**string**       | Powerup ID Length  <br>**byte**     | Powerup ID  <br>**string**     |                                     |                                     |                                |                           |                            |                       |
| 0x02 | SpawnBomb            | Name Length  <br>**byte** | Name  <br>**string** | Tile X Length  <br>**byte**        | Tile X  <br>**string**              | Tile Y Length  <br>**byte**    | Tile Y  <br>**string**       | Powerup ID Length  <br>**byte**     | Powerup ID  <br>**string**     | Radius Length  <br>**byte**         | Radius  <br>**string**              | Burn Time Length  <br>**byte** | Burn Time  <br>**string** | Timer Length  <br>**byte** | Timer  <br>**string** |
| 0x03 | SpawnTimeBomb        | Name Length  <br>**byte** | Name  <br>**string** | Tile X Length  <br>**byte**        | Tile X  <br>**string**              | Tile Y Length  <br>**byte**    | Tile Y  <br>**string**       | Timer Length  <br>**byte**          | Timer  <br>**string**          |                                     |                                     |                                |                           |                            |                       |
| 0x04 | SpawnTimeDoor        | Name Length  <br>**byte** | Name  <br>**string** | Tile X Length  <br>**byte**        | Tile X  <br>**string**              | Tile Y Length  <br>**byte**    | Tile Y  <br>**string**       | Timer Length  <br>**byte**          | Timer  <br>**string**          |                                     |                                     |                                |                           |                            |                       |
| 0x05 | SpawnLockedDoor      | Name Length  <br>**byte** | Name  <br>**string** | Tile X Length  <br>**byte**        | Tile X  <br>**string**              | Tile Y Length  <br>**byte**    | Tile Y  <br>**string**       | Key ID Length  <br>**byte**         | Key ID  <br>**string**         |                                     |                                     |                                |                           |                            |                       |
| 0x06 | SpawnKey             | Name Length  <br>**byte** | Name  <br>**string** | Tile X Length  <br>**byte**        | Tile X  <br>**string**              | Tile Y Length  <br>**byte**    | Tile Y  <br>**string**       | Key ID Length  <br>**byte**         | Key ID  <br>**string**         |                                     |                                     |                                |                           |                            |                       |
| 0x07 | Blast                | Name Length  <br>**byte** | Name  <br>**string** | Tile X Length  <br>**byte**        | Tile X  <br>**string**              | Tile Y Length  <br>**byte**    | Tile Y  <br>**string**       | BlastType ID Length  <br>**byte**   | BlastType ID  <br>**string**   | Radius Length  <br>**byte**         | Radius  <br>**string**              | Burn Time Length  <br>**byte** | Burn Time  <br>**string** |                            |                       |
| 0x08 | PlayerMessage        | Name Length  <br>**byte** | Name  <br>**string** | Text Length  <br>**ushort**        | Text  <br>**string**                | Player ID Length  <br>**byte** | Player ID  <br>**string**    | Duration Length  <br>**byte**       | Duration  <br>**string**       |                                     |                                     |                                |                           |                            |                       |
| 0x09 | TileMessage          | Name Length  <br>**byte** | Name  <br>**string** | Text Length  <br>**ushort**        | Text  <br>**string**                | Tile X Length  <br>**byte**    | Tile X  <br>**string**       | Tile Y Length  <br>**byte**         | Tile Y  <br>**string**         | Duration Length  <br>**byte**       | Duration  <br>**string**            |                                |                           |                            |                       |
| 0x0a | TickerMessage        | Name Length  <br>**byte** | Name  <br>**string** | Text Length  <br>**ushort**        | Text  <br>**string**                |                                |                              |                                     |                                |                                     |                                     |                                |                           |                            |                       |
| 0x0b | RemoveBomb           | Name Length  <br>**byte** | Name  <br>**string** | Tile X Length  <br>**byte**        | Tile X  <br>**string**              | Tile Y Length  <br>**byte**    | Tile Y  <br>**string**       |                                     |                                |                                     |                                     |                                |                           |                            |                       |
| 0x0c | RemovePowerup        | Name Length  <br>**byte** | Name  <br>**string** | Tile X Length  <br>**byte**        | Tile X  <br>**string**              | Tile Y Length  <br>**byte**    | Tile Y  <br>**string**       |                                     |                                |                                     |                                     |                                |                           |                            |                       |
| 0x0e | Delay                | Name Length  <br>**byte** | Name  <br>**string** | Timer Length  <br>**byte**         | Timer  <br>**string**               |                                |                              |                                     |                                |                                     |                                     |                                |                           |                            |                       |
| 0x0f | IfCondition          | Name Length  <br>**byte** | Name  <br>**string** | Operation  <br>**byte**            | Value 1 Length  <br>**byte**        | Value 1  <br>**string**        | Value 2 Length  <br>**byte** | Value 2  <br>**string**             | Link Count  <br>**ushort**     | Command Link IDs  <br>**ushort(s)** |                                     |                                |                           |                            |                       |
| 0x10 | LoopCommand          | Name Length  <br>**byte** | Name  <br>**string** | Loop Start Length  <br>**byte**    | Loop Start  <br>**string**          | Loop End Length  <br>**byte**  | Loop End  <br>**string**     | Loop Increment Length  <br>**byte** | Loop Increment  <br>**string** | Link Count  <br>**ushort**          | Command Link IDs  <br>**ushort(s)** |                                |                           |                            |                       |
| 0x11 | SetVariable          | Name Length  <br>**byte** | Name  <br>**string** | Variable Name Length  <br>**byte** | Variable Name  <br>**string**       | Value Length  <br>**byte**     | Value  <br>**string**        |                                     |                                |                                     |                                     |                                |                           |                            |                       |
| 0x12 | SetLocalVariable     | Name Length  <br>**byte** | Name  <br>**string** | Variable Name Length  <br>**byte** | Variable Name  <br>**string**       | Value Length  <br>**byte**     | Value  <br>**string**        |                                     |                                |                                     |                                     |                                |                           |                            |                       |
| 0x13 | TeleportPlayer       | Name Length  <br>**byte** | Name  <br>**string** | Player ID Length  <br>**byte**     | Player ID  <br>**string**           | Tile X Length  <br>**byte**    | Tile X  <br>**string**       | Tile Y Length  <br>**byte**         | Tile Y  <br>**string**         |                                     |                                     |                                |                           |                            |                       |
| 0x14 | HitPlayer            | Name Length  <br>**byte** | Name  <br>**string** | Player ID Length  <br>**byte**     | Player ID  <br>**string**           |                                |                              |                                     |                                |                                     |                                     |                                |                           |                            |                       |
| 0x15 | KillPlayer           | Name Length  <br>**byte** | Name  <br>**string** | Player ID Length  <br>**byte**     | Player ID  <br>**string**           |                                |                              |                                     |                                |                                     |                                     |                                |                           |                            |                       |
| 0x17 | LinkCommand          | Name Length  <br>**byte** | Name  <br>**string** | Link Count  <br>**ushort**         | Command Link IDs  <br>**ushort(s)** |                                |                              |                                     |                                |                                     |                                     |                                |                           |                            |                       |
| 0x18 | StopRunner           | Name Length  <br>**byte** | Name  <br>**string** |                                    |                                     |                                |                              |                                     |                                |                                     |                                     |                                |                           |                            |                       |
| 0x19 | StopTrigger          | Name Length  <br>**byte** | Name  <br>**string** |                                    |                                     |                                |                              |                                     |                                |                                     |                                     |                                |                           |                            |                       |
| 0x1a | DisableTrigger       | Name Length  <br>**byte** | Name  <br>**string** |                                    |                                     |                                |                              |                                     |                                |                                     |                                     |                                |                           |                            |                       |
| 0x1b | SetTemporaryVariable | Name Length  <br>**byte** | Name  <br>**string** | Variable Name Length  <br>**byte** | Variable Name  <br>**string**       | Value Length  <br>**byte**     | Value  <br>**string**        |                                     |                                |                                     |                                     |                                |                           |                            |                       |

Variable Section
----------------

This section defines Variables for the User Space. The data of an entry is structured as follows.

| Data Structure            |                      |                            |                                |                               |
|---------------------------|----------------------|----------------------------|--------------------------------|-------------------------------|
| Name Length  <br>**byte** | Name  <br>**string** | Start Value  <br>**float** | Underflow Value  <br>**float** | Overflow Value  <br>**float** |