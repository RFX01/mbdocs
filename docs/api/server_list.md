---
layout: default
title: Server List
parent: API
nav_order: 2
---

The MadBomber API provides an interface for publicly listing MadBomber Gameservers. Administrators running the Dedicated Server can choose to have their server register itself on the API, which will make it appear on the public server list. Availability of the server will be verified by the API via a separate utility called mbapiconncheck to ensure all listed servers are online and publicly reachable.

### API Methods

* * *

The register method is used by the dedicated server to register themselves for the Server List. Once the register Request is received, the API will attempt to establish a connection to the gameserver on the request IP at the specified port. If this connection is successful, there is an additional returned parameter called **uuid**, which contains the UUID assigned to the server. This UUID will be used for servers to authenticate themselves to the API.

#### Parameters

**name** \- The name of the server as configured by the admin  
**port** \- The port of the server as configured by the admin  
**max_players** \- The total amount of players allowed in the lobby at once  
**lobby_state **\- The current state of the lobby, Idle/Initializing/Ingame  
**map_count** \- The total amount of loaded maps on the server  
**game\_type\_count** \- The total amount of loaded game types on the server  
**region** \- The server region as configured by the admin

#### Returns

Returns a single object with the following properties:

**status** \- Short string to sum up the registration result, can be either "Accepted", "Already Registered" or "unreachable".  
**message** \- A message to be displayed to the server admin via the console

* * *

After registration, the update method is expected to be called regularly by the dedicated server to confirm they are still online and update their status. If a server fails to send this request after a minute, it will be hidden from the server list. If a server does not send an update within 30 days after initial registration, it will be permanently removed from the server list.

#### Parameters

**name** \- The name of the server as configured by the admin  
**port** \- The port of the server as configured by the admin  
**uuid** \- The UUID received upon registration, required for update to be accepted  
**current_players** \- The current amount of players in the lobby**max_players** \- The total amount of players allowed in the lobby at once  
**lobby_state **\- The current state of the lobby, Idle/Initializing/Ingame  
**map_count** \- The total amount of loaded maps on the server  
**game\_type\_count** \- The total amount of loaded game types on the server  
**region** \- The server region as configured by the admin

#### Returns

Returns a single object with the following properties:

**status** \- Short string to sum up the registration result, can be either "accepted", "unknown" or "unreachable".  
**message** \- A message to be displayed to the server admin via the console

* * *

This method will return multiple objects representing all currently online servers registered on the MadBomber API.

#### Returns

Each returned object has the following properties:

**name** \- The name of the server as configured by the admin  
**ip** \- The IP on which the server can be reached  
**port** \- The Port the game server is running on  
**current_players** \- The current amount of players in the lobby**max_players** \- The total amount of players allowed in the lobby at once  
**lobby_state **\- The current state of the lobby, Idle/Initializing/Ingame  
**map_count** \- The total amount of loaded maps on the server  
**game\_type\_count** \- The total amount of loaded game types on the server  
**region** \- The server region as configured by the admin