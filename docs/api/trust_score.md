---
layout: default
title: Trust Score
parent: API
nav_order: 2
---

The MadBomber API calculates a so called "Trust Score" for every registered player. This score represents the trustworthiness of the player in regards to their behavior. This score is represented as a numeric value. Server Administrators can configure their servers so that a players Trust Score has to be above a configurable threshold to be allowed on their server.

Negative behavior of players will be punished by reducing the Trust Score of said player. This is intended to discourage negative behavior by preventing those people from joining certain public servers. With this method, those players should generally get grouped together on servers that have a lower Trust Score requirement, with the more trustworthy players playing on a server with higher Trust Score requirements.

Trust Ranks
-----------

In order to help players understand the Trust Score system, different Trust Score ranges will have a Trust Rank associated with it. This essentially just provides a label for a certain Trust Score range to get a better idea on what kind of players you can expect to find in a given range.

| Icon | Rank Name | Range (inclusive) |
|------|-----------|-------------------|
|      | Ultimate  | 150 and above     |
|      | Veteran   | 125 to 149        |
|      | Advanced  | 110 to 124        |
|      | Standard  | 90 to 109         |
|      | Tainted   | 70 to 89          |
|      | Untrusted | 30 to 69          |
|      | Sketchy   | 29 and below      |

Loosing Trust Score
-------------------

There are numerous actions that can negatively impact a players Trust Score.

When a player gets banned on a public server, their Trust Score will be reduced by 5 points. As anyone can ban another player from their server without any review, this penalty is not very large. Players can however submit a Report against a Server Admin for pointless bans.

Another way for a player to loose Trust Score is having reports submitted against them. Once a report is initially created, their Trust Score will be reduced by 1 point unless the player creating the report has created false or abusive reports recently. If the report is acknowledged by RFX, their Trust Score will be reduced by an amount decided on a case-by-case basis.

If a players report is deemed to be false or abusive, the trust score of the reporting player will be reduced by 5 to 50 points, depending on the severity of the case.

Gaining Trust Score
-------------------

A newly registered player will start with a Trust Score of 100. In order to reward players for playing fairly, Trust Score can be recovered by simply playing the game. Every two hours of ranked gameplay, 1 point of Trust Score will be recovered. This will make one-time incidents less of a big deal and effectively allows players to recover Trust Score infinitely.

This mechanic also allows for a players Trust Score to exceed 100, which Server Administrators can use in order to require a certain amount of Playtime for Players to be able to join their servers. This can be used to create servers where more experienced players can play against opponents closer to their own level, keeping the matches interesting. Since newer players are forced to play on servers that permit accounts with little to no playtime to join, the likelihood of them running into players way above their skill level is reduced.

Valid Report Reasons
--------------------

There are various situations in which a players behavior is considered negative and should be reported. This sections lists any valid reasons I can think of, although reports for other reasons can still be accepted as valid if the reason provided by the reporter is sufficient.

### API Manipulation Attempts

This can include smaller things such as excessive Idling, where a player would repeatedly join in on Matches but never actually do anything, purely as a means to increase their Trust Score from the recorded Playtime. This is probably the least severe of such attempts, which would result in a smaller deduction between 5 and 10 Trust Score points.

More severe reasons would include setting up multiple accounts and abusing the extra accounts to record match wins on their main account. If servers with many idle accounts are spotted, the Accounts on this server should be reported immediately. Such a manipulation attempt will result in a global ban of all extra accounts and a Trust Score deduction between 10 and 30 points, depending on the situation. Any matches that included those fake accounts would also be invalidated, likely resulting in further Trust Score deduction from the reduced Playtime.

The most severe manipulation attempt would be accessing the API via custom Scripts or maliciously modified Game Clients / Servers (hacks). Depending on the severity of the case, there will either be a large deduction in trust score (above 30 points) or an outright global ban, possibly including IP-Blackholing and any other necessary network-related measures as well.

### False Banning/Reporting

Anyone who runs a server can also ban people from their server. However, these bans are expected to be justifiable and have a reasonable timeframe associated with them. The reason for that being that bans will negatively affect a players Trust Score immediately, as a means to prevent players from going on a rampage while the "mods are asleep". Any player who gets banned on a Server can submit a report for the Server owner if they believe the ban was unjustified. If a ban is decided to be unjustified, the Server owner will receive a Trust Score penalty between 5 and 15 points. Any unjustified bans will be lifted immediately.

In addition to false bans, false reports will also result in a penalty. However, this generally does not have to be reported by players, as false reports should be noticed during review. If they somehow manage to slip under the radar, players can still be reported for false reports, in which case the penalty may be much more severe. If a players report is deemed to be false during review, any future reports from said player will not negatively affect the reported players Trust Score until the report has been manually reviewed.

### Content Reupload

This is related to Content submitted to the Master Content Repository. If a player decides to submit a direct copy of another players map without significant modifications, they will receive a Trust Score penalty between 5 and 15 points, depending on the severity of the case. The corresponding map submission will also be fully deleted from the API, and any matches that were played on it will be invalidated.

For GameTypes, there is too little variation between them to seriously accuse someone of theft. If one turns out to be a really obvious reupload, the same penalty as for Map reuploads applies. Although generally speaking, reports for very similar GameTypes should be avoided. A report for a GameType should only be created if the GameType is provably a Reupload of an existing GameType with no Map linked to it.

### General Misbehavior

This is intentionally broad, as it would be close to impossible to comprehensively list everything someone could be doing wrong. This is essentially the category that sums up what you may refer to as "the usual rules". Such misbehavior can include things such as sending toxic chat messages, hosting Servers or creating Maps/GameTypes with excessively offensive Names/Descriptions and any other kind of toxic behavior towards other players.

Since what is considered offensive can vary greatly from person to person, the outcome of these reports will depend on the people involved. Any penalties are decided on a case-by-case basis, depending on the amount of people involved and the amount of trouble that has been caused.