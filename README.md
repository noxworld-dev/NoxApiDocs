## OpenNox Lua Modding API

Draft version.

The main idea of the Lua API is based around manipulating in-game entities (Units) by use of common methods/functions, regardless of their real in-game type.
For example, you can make a static Object (statue for example) cast a Spell, and it will do so; just as well you can make a Monster cast a Spell, and it will do so too, with single difference of doing an animation for that.
Parts of the API are comparable in their naming and effects to the good old Nox Map editor scripting engine.

Currently, the following namespaces and functions are exposed by the Lua API:
```
Nox.Audio
Nox.Players
Nox.Object
Nox.ObjectType
Nox.FrameTimer
Nox.SecondTimer
Nox.Timer
Nox.Wall
Nox.Waypoint
```

The following types of entities are declared within the Lua API:
```
Unit
UnitGroup
Object
ObjectGroup
Wall
WallGroup
Waypoint
Timer
```

