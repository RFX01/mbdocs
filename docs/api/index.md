---
layout: default
title: API
nav_order: 4
has_children: true
---

The MadBomber API will provide public information to complement the game.

Features
========
* Player Registration
* Public Gameserver List
* Public Map & Game Type Repository
* Global Statistics

Validations
===========

* Ensure MBDS is reachable when server is registered and updated
* Ensure Player is authenticated before joining public server lobby
* Ensure joining Player does not exceed the servers player limit
* Ensure Server is online when match is submitted
* Ensure Server is authenticated when match is submitted
* Ensure submitted match duration is shorter than the time between last submitted match and now
* Ensure first submitted match duration is not absurdly long (>30 minutes)
* Ensure all participating players are on the server when match is submitted
* Ensure Player does not join two public lobbies at the same time
* Ensure unique names for Maps & GameTypes
* Ensure User Agent makes sense for the Request that is being made

Data Structure
==============
![](/assets/img/net/mbapi-data-structure.png)

Objects
=======

### Server

Stores a Server that has registered itself on the MadBomber API.

| Type     | Name              | Description                                                                                                                          |
|----------|-------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| string   | name              | The Name of the sever as configured by it's Admin.                                                                                   |
| string   | ip                | The IP of the server for clients to connect to. Taken from the Header of the registration request.                                   |
| integer  | port              | The Port of the server for clients to connect to as reported on registration.                                                        |
| string   | client_version    | The Game Client version expected by the server.                                                                                      |
| string   | uuid              | The UUID assigned to the server on registration. Effectively used like a Username for authentication.                                |
| string   | auth_key          | 512-bit Key used like a password for authentication. Stored as an argon2 hash.                                                       |
| integer  | max_players       | Player Limit as reported by the server.                                                                                              |
| integer  | current_players   | Currently active player count as reported by the server.                                                                             |
| integer  | trust_requirement | The minimum Trust Score required for Players to join this server.                                                                    |
| string   | lobby_state       | A string to indicate the state of the lobby. Can be either Idle, Initializing or Ingame.                                             |
| integer  | map_count         | The amount of loaded maps as reported by the server.                                                                                 |
| integer  | game\_type\_count | The amount of loaded gametypes as reported by the server.                                                                            |
| string   | region            | A string to indicate the physical location of a server for the purpose of selecting a nearby server.                                 |
| boolean  | online            | Set to true if the server is reachable by the API. If this is set to false, the server will not be listed on the server list.        |
| datetime | last_update       | The last time an update from the server has been received. Used to ensure server aren't offline for too long.                        |
| datetime | register_time     | The time at which the server was first registered on the API.                                                                        |
| datetime | online_since      | The time at which the server reporter its startup. Effectively contains the last restart time. Can also be used to calculate uptime. |
| Player   | owner             | The player who owns this server.                                                                                                     |

  

### Player

Stores a Player that has registered themselves on the MadBomber API.

| Type     | Name              | Description                                                                                                                                                                |
|----------|-------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| string   | name              | The players chosen nickname. Uniqueness is enforced.                                                                                                                       |
| string   | uuid              | The UUID assigned to the player on registration. Effectively used like a Username for authentication.                                                                      |
| string   | auth_key          | 512-bit Key used like a password for authentication. Stored as an argon2 hash.                                                                                             |
| string   | last_ip           | The Last IP the Player has logged in with.                                                                                                                                 |
| integer  | submission_limit  | The maximum combined amount of unique Maps and GameTypes that the player is allowed to upload.                                                                             |
| bool     | global_ban        | Can be set to true to globally ban a player. A global ban prevents players from joining public lobbies and submitting maps/gametypes. Reserved for emergencies.            |
| bool     | admin             | Defines this user as an API Admin. This will grant some minor benefits such as not being able to get reported and getting Nickname validations bypassed. Reserved for RFX. |
| bool     | bypass\_ip\_limit | This will bypass the IP Check for this player, effectively allowing another account to be registered from the same IP as this player.                                      |
| datetime | register_time     | The time at which the player was registered on the API.                                                                                                                    |
| datetime | last_activity     | The last time anything has been done by the player. Updated any time the player is successfully authenticated.                                                             |
| Server   | connected_server  | If the player is currently in a public server lobby, this will contain the server the player is currently connected to.                                                    |

  

### Match

Stores the outcome of a ranked match played on a public server.

| Type     | Name         | Description                                                       |
|----------|--------------|-------------------------------------------------------------------|
| decimal  | playtime     | The total length of the match in seconds.                         |
| datetime | submitted_at | The time at which this match result was submitted.                |
| Player   | winner       | The Player who won this match. Set to null if the match was tied. |
| Map      | map          | The map this match was played on.                                 |
| GameType | game_type    | The game type this match was played with.                         |
| Server   | server       | The server this match was played on.                              |

  

### JoinToken

Stores a token that is used for validating Players every time they attempt to join a public lobby.

| Type     | Name        | Description                                                                                 |
|----------|-------------|---------------------------------------------------------------------------------------------|
| string   | token       | A 192-bit Hex string representing the token.                                                |
| bool     | validated   | If the player authenticates themselves within a valid timeframe, this will be set to true.  |
| Player   | player      | The player who reported themselves to the server.                                           |
| Server   | server      | The server that requested the JoinToken.                                                    |
| datetime | valid_until | Defines when the Token will expire. Typically set to a few seconds after the creation time. |
| datetime | created_at  | The time at which the Token was requested.                                                  |

  

### MatchPlayer

Stores a players participation in a Match along with some stats.

| Type    | Name               | Description                                                                    |
|---------|--------------------|--------------------------------------------------------------------------------|
| Match   | match              | The match the player participated in.                                          |
| Player  | player             | The player who participated in the match.                                      |
| integer | painted_tiles      | The amount of tiles painted by the player. Only used for Paint Bomb GameTypes. |
| integer | broken_tiles       | The amount of tiles broken by the player.                                      |
| integer | placed_bomb        | The amount of bombs placed by the player.                                      |
| integer | used_abilities     | The amount of abilities used by the player (counter per use).                  |
| integer | collected_powerups | The amount of powerups collected by the player.                                |

  

### MatchKill

Stores a kill that occurred during a match.

| Type        | Name          | Description                                     |
|-------------|---------------|-------------------------------------------------|
| MatchPlayer | match_player  | The MatchPlayer object of the killing player.   |
| Player      | killed_player | The Player object of the killed player.         |
| decimal     | kill_time     | The time at which the kill occurred in seconds. |

  

### Map

Stores a map submitted to the API by a player.

| Type     | Name         | Description                                                                                                                                                   |
|----------|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| string   | name         | The filename of the map (including the File Extension). Uniqueness is enforced.                                                                               |
| string   | description  | A description provided by the mapper to store additional information about the map.                                                                           |
| string   | uuid         | A UUID assigned to the map used for identifying map objects across versions. Can be referenced in the server configuration to download the map automatically. |
| string   | checksum     | Contains a SHA256 Checksum of the map stored as a Base64 string.                                                                                              |
| integer  | version      | A number representing the Map Version. Starts at 1 and is incremented for every new version.                                                                  |
| string   | mbm_file     | This field is used to store the MBM File using ActiveRecord.                                                                                                  |
| integer  | size_x       | The Size of the map on the X Axis                                                                                                                             |
| integer  | size_y       | The Size of the map on the Y Axis                                                                                                                             |
| integer  | spawn_count  | The amount of SpawnPoints on the map.                                                                                                                         |
| string   | image_file   | This field is used to store the preview image using ActiveRecord.                                                                                             |
| datetime | submitted_at | The time at which this version of the map was submitted.                                                                                                      |
| Player   | creator      | The player who created the map.                                                                                                                               |
| Map      | new_version  | References the new version of the map. Set to null on the latest version.                                                                                     |

  

### GameType

Stores a GameType submitted to the API by a player.

| Type     | Name         | Description                                                                                                                                                             |
|----------|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| string   | name         | The filename of the Game Type (including the File Extension). Uniqueness is enforced.                                                                                   |
| string   | description  | A description provided by the creator to store additional information about the GameType.                                                                               |
| string   | uuid         | A UUID assigned to the GameType used for identifying GameType objects across versions. Can be referenced in the server configuration to download the map automatically. |
| string   | checksum     | Contains a SHA256 Checksum of the GameType stored as a Base64 string.                                                                                                   |
| integer  | version      | A number representing the GameType Version. Starts at 1 and is incremented for every new version.                                                                       |
| string   | xml_file     | This field is used to store the XML File using ActiveRecord.                                                                                                            |
| datetime | submitted_at | The time at which this version of the GameType was submitted.                                                                                                           |
| Player   | creator      | The player who created the GameType.                                                                                                                                    |
| Map      | new_version  | References the new version of the GameType. Set to null on the latest version.                                                                                          |

  

### ServerBan

Stores a ban of a player submitted by a server admin.

| Type     | Name         | Description                                                                  |
|----------|--------------|------------------------------------------------------------------------------|
| Player   | player       | The player who was banned from the server.                                   |
| Server   | server       | The server the player is banned from.                                        |
| string   | message      | A message provided by the server admin as the ban reason.                    |
| datetime | banned_at    | The time at which the player was banned.                                     |
| datetime | banned_until | The time at which the ban will be lifted. Limited to 10 years in the future. |

  

### PlayerReport

Stores a report against a player submitted by another player.

| Type     | Name             | Description                                                                                                                                                   |
|----------|------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Player   | reporting_player | The player who submitted the report.                                                                                                                          |
| Player   | reported_player  | The player who got reported.                                                                                                                                  |
| text     | message          | A message to explain why the report was submitted.                                                                                                            |
| integer  | trust_impact     | How much Trust Score is deducted for the report. This deduction is only applied if the report has already been acknowledged.                                  |
| bool     | is_acknowledged  | Used to confirm that RFX took a look at the report and deemed it valid. When this is set, the report will negatively affect the reported players trust score. |
| bool     | is_false         | Used to flag false reports. If RFX deemed a report to be false or abusive, this will be set and negatively affect the reporters trust score.                  |
| datetime | report_time      | The time at which the report was submitted.                                                                                                                   |
| datetime | acknowledge_time | The time at which the report was acknowledged.                                                                                                                |