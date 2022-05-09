
Nox Lua Modding Api (NoxApi)
===
Draft version of the modding API docs for OpenNox.

API structure
---
Namespaces
---
### Client 
Incapsulates every function that is related to client interface / game client.
A client-side mod can: 
* iterate players in a current match;
* capture custom signals from another server mod on a network bus;
* capture, process and block key and mouse events;
* capture some critical events, like MapChange, PlayerJoinServer, PlayerLeaveServer, PlayerDie;
* display some useful info on the screen, play sounds;
* load custom resources like images and sounds. 

Classes:
```
State
GameWindow
Renderer
Music
ClientObject/Entity/Sprite
ClientWorld/Map
PlayerSaveData
Player (read-only access for client)
```
### Server
Hosts everything that is related to the server side and game state processing.
A server-side mod can: 
* iterate players in a current match, ban or kick them;
* iterate, create and delete teams in MP game, move players between them;
* override the current game rules, change lesson limit;
* change the current game mode or the map, iterate all maps' names;
* fully manipulate objects/entities in the game world;
* capture, process and block all in-game events, for example, OnScriptCalled, OnScoreChanged, OnTeamJoin;
* modify state of any player in the game, teleport them, force them into or out of the observer mode;
* iterate mods that are installed on any client that joins this server, and send custom messages to the clients.

Classes:
```
State
Match/MatchRules
Object/Entity
World/Map
Player
```
### Common
Hosts all data that is required for both client and server mods.

Classes:
```
Environment (no filesystem access)
Constants
DataStorage
ItemModifier
MonsterData
ImageData
SoundData
ThingData
Team
Connection (different for client and server, used for communication between mods)
```

Mod Structure and lifecycle
---
Each mod is thought of as a Zip file, that contains: 
* text manifest that describes the specified mod;
* one or more Lua files that modify the game's logic;
* probably some external resources, like images and music.


