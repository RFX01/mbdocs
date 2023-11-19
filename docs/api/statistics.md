---
layout: default
title: Statistics
parent: API
nav_order: 2
---

The MadBomber API is going to collect various statistics about different aspects of the game and the community. These stats are meant to be viewed on MadBomber.NET

After the end of every Match, the Server will report the Match end to the API, along with all relevant parameters about the match, such as which server is sending the report, who was playing, which Map and Game Type was used and who won the match. These statistics can then be used to determine popularity of Servers, Maps and Game Types. They might also be useful in the future for the purpose of adding rankings.

Using just these Match End stats, it would also be possible to build stats for users, such as the last Server/Map/GameType Combo they played on, their total playtime (also possible per server/map/gametype) and their Win/Loss ratio.