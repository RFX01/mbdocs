---
layout: default
title: Player Registration
parent: API
nav_order: 2
---

The MadBomber API provides an interface for users to register and authenticate themselves. 

Registration will be done within the Game Client. A Player simply has to enter a Username and the game will attempt to register the Player on the API with the name set by the user. This would generally succeed unless there is already a player registered with the same Username. Once registration succeeds, the Client will receive a UUID and an authorization key, which is going to be saved in a file. This file will also be accessed by the Map Editor for submitting Maps and Game Types. The Username could be changed at any time.

With a system like this in place, it might be a good idea to remove accounts after a certain period of inactivity. Additionally, there should be something in place to prevent too many players from being registered from the same IP. This would be to prevent general spam, not that spammers would have anything to gain from spamming the Player database. On top of that, since there won't be a Web Frontend for registration or public API Documentation, this should fly under the radar of a lot of spammers.

**2023 Update:** Looking back at this old idea, perhaps it would make more sense to implement a simple 'login with discord' option. Having this no effort instant registration system might be nice, but in reality it has caused more issues than benefits. It also failed at making players get into the game, as learning the game is a far larger hurdle than registering an account would be. I'll probably deprecate the instant registration system in favor of a more involved system that requires you to login with discord, as I assume every player will have a discord account.

JoinToken Handling
------------------

Whenever a registered Player wants to join a public server, they first need to be verified against the API before the server will permit them to join the lobby. This is implemented using a JoinToken, which is requested by a Server, sent to a client, which then uses it to authenticate itself against the API, tells the server about it and if everything is valid, the Player will be allowed to join the Lobby.

![](/assets/img/net/mbapi-jointoken-flow.png)