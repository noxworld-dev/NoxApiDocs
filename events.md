## Nox Lua Modding Api (NoxApi)
### Events

```
require 'Nox.Events'
```
Available: `Server`, `Client`

Event bus manipulation functions:
```
RegisterEvent(eventName, eventHandler)
UnregisterEvent(eventHandler)
FireEvent(eventName, eventArgs)
```

List of events available to all mods (client and server):
```
PlayerLeave(PlayerId)
PlayerJoin(PlayerId)
PlayerDie(Player)
PlayerChat(Player, Text)
FrameTick()
MatchEnded()
MapLoaded(MapName)
```

List of events that are available exclusively to server mods:
```
NativeScriptRun(ScriptName)
PlayerObserverChange(PlayerId, NewObsState)
PlayerInteractTrigger(Player, Object)
PlayerPickupObject(Player, Object)
PlayerDropObject(Player, Object)
JoinedTeam(Player, Team)
LeftTeam(Player, Team)
TeamCreated(Team)
TeamDeleted(Team)
```

### TODO:
More events:
Quest/Gauntlet games? 
Polygon enter/leave?
Monster events?
