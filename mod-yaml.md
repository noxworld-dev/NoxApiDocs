## Nox Lua Modding Api (NoxApi)
### Mod file structure 

Example:

```
mod:
 - name: example
 - available: client
 - maintainer: angrykirc
 - mainfile: main.lua
 - version: 1.0
```

A single mod file cannot be available both on server and client sides.
If you want to create a mod that extends both client and server functionality, you will have to separate it into two packages.
This restriction is made in order to improve code quality and maintainability.

```
mod:
 - name: example_client
 - available: client
 - maintainer: angrykirc
 - mainfile: main.lua
 - version: 1.0
```

```
mod:
 - name: example_server
 - available: server
 - maintainer: angrykirc
 - mainfile: main.lua
 - version: 1.0
```
