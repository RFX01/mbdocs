---
layout: default
title: Master Content Repository
parent: API
nav_order: 2
---

The MadBomber API provides an interface for publicly listing Content such as Maps and Gametypes. 

Maps and Game Types will be submitted using a Dialog on the Map Editor. The location where a player can edit their submissions has yet to be decided.

Once a Map is received, the file will be stored using ActiveRecord. Additionally, the MBM File will be parsed in order to get the Metadata from the header and generate a preview image from the Tile Block. The preview image will also be stored using ActiveRecord.

For Gametypes, the XML File will be stored using ActiveRecord. Details about a Game Type can be requested. On this request, the XML will be parsed and all individual parameters are returned. This can be used for displaying all details about a Game Type on the Website, which will allow players to check out the properties of a game type before they play it.

Both Maps and Game Types will have a Name and Description field. The name is based off the filename and can't be changed once uploaded. The description can be freely set by the user and updated whenever they want. Any submitted items can also be deleted whenever the user wants. Once deletion is requested, the file will be hidden from the public list. At this point, the user can choose to restore the deleted item for 30 days, after which it will be permanently deleted.

Maps and Game Types can be updated by their creators. The old versions will still be kept so it can be reverted to if required. Additionally, players can choose to keep playing using old versions of Maps and Game Types.

Any publicly listed Maps and Game Types can be added to a server without downloading them beforehand. There will be a configuration option within the server configuration that can be used to specify a list of Maps and Game Types from the Master Repository. These will then be automatically downloaded before the Content on the server is loaded. These entries can also specify a specific Map/GameType version. If no versions are specified, the Maps and Game Types will automatically be updated on server startup if an update is available.