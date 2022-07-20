## Nox Lua Modding Api (NoxApi)

Draft version of the modding API docs for OpenNox.

The entire API is split into five major namespaces, which can be requested by the mods in runtime.
You can also execute Lua commands via Nox console at any time by simply typing `$ command`.

### Client 

```
require 'Nox.Client'
```
Incapsulates every function that is related to client interface / game client.
A client-side mod can: 
* iterate players in a current match;
* capture custom signals from another server mod on a network bus;
* capture, process and block key and mouse events;
* capture some critical events, like MapLoaded, PlayerJoin, PlayerLeave, PlayerDie;
* display some useful info on the screen, play sounds;
* load custom resources like images and sounds. 

Classes:
```
CliObject -> GetThingDef(), .x, .y etc.
Window -> AddEvent(), .x, .y, .w, .h
Client (static) -> CreateWindow(), DestroyWindow()
```

### Server

```
require 'Nox.Server'
```
Contains everything that is related to the server side and game state processing.
A server-side mod can: 
* iterate players in a current match, ban or kick them;
* iterate, create and delete teams in MP game, move players between them;
* override the current game rules, change lesson limit;
* change the current game mode or the map, iterate all maps' names;
* fully manipulate objects/entities in the game world;
* capture, process and block all in-game events, for example, NativeScriptRun, ScoreChanged, JoinedTeam;
* modify state of any player in the game, teleport them, force them into or out of the observer mode;
* iterate mods that are installed on any client that joins this server, and send custom messages to the clients.

Static classes:
```
Map -> GetInfo(), CreateObject(), GetObject(), GetWaypoint(), GetWall(), MakeSound() etc.
Object -> CheckClass(), Move(), Delete(), DeleteDecay() 
Server -> Ban(), Kick(), ChangeGameMode(), ChangeMap()
```
### Media

```
require 'Nox.Media'
```
Contains all data and declarations that are required for both client and server mods.
Some may be unavailable in headless server mode.

Static classes:
```
ThingDb -> GetThingDef(), ThingDef, SpellDef etc.
VideoDb -> RegisterImage(), GetImage()
AudioDb -> RegisterSound(), GetSound()
```

All custom resources will be automatically unloaded when the mod that added them is unloaded.


### Common

```
require 'Nox.Common'
```
Classes and functions that are shared between both client and server mods.

Static classes:
```
Match -> GetPlayers(), GetTeams(), GetPlayerByName(), GetPlayerById() etc.
Math -> BitAnd(), BitOr(), BitXor(), Distance(), DistanceSq()
Log -> Printf(), PrintfColor()
Modifier -> RegisterModifier(), GetModifier()
Buffs -> 
Spells ->
Abilities ->
```

### Event handlers

```
require 'Nox.Events'
```
Any mod can register an event handler to listen for [in-game events](events.md).

Basic event bus example:
```
event=1
event=function() print("New map loaded!") UnregisterEvent(event) end
RegisterEvent("MapLoaded", event)
```

All events on the bus will be automatically unloaded when the mod that added them is unloaded.

You can register sub-events for specific in-game objects (like OnCollide() for Objects)
These sub-events also have no need to be cleaned up manually, the scripting engine manages them on its own.


### Lifetime of classes

Some classes (like Player, Object) are declared invalid ("expired") upon certain events or in-game circumstances.
For example, when a Player leaves the server, all corresponding objects that are linked to this Player will be declared invalid, and any call to any property of such class will raise an error.
You can check the validity of any such class at any time by calling .IsValid() or .valid method or property.
Lifetime of such classes is kept internally tracked by the scripting engine by assigning a GUID for each instance of created object and listening to the destruction events (PlayerLeave for Players for example).
Whenever any method of such class is called, its GUID is tested against the database of known active GUIDs.
If GUID wasn't found in the database, the given class instance counts as expired.

### Mod Structure and lifecycle

See [mod file structure](mod-yaml.md).

Each mod is thought of as a Zip file, that contains: 
* .yaml manifest that describes the specified mod;
* one or more Lua files that modify the game's logic;
* probably some external resources, like images and music.

### TODO:

Server-to-client network pipes for custom data?


