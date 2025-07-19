# bedrock-server
A simple Docker compose file for a Minecraft Bedrock server

## Prerequisites

Docker - see here for installation instructions: https://docs.docker.com/engine/install/

## Configuration

Data files should be placed in `./data/`, e.g.:

```
|-- .env
|-- LICENSE
|-- README.md
|-- data
|   |-- allowlist.json
|   |-- data\ files\ go\ here!
|   |-- permissions.json
|   |-- server.properties
|   `-- worlds
|       `-- <WorldName>
`-- docker-compose.yml
```

where 

- `data/worlds/`: should contain the world directory; `<WorldName>` would be the name of the world folder being use, and should be onted for a later stage.
- `data/allowlist.json`: this is the allow list for the server to say who can gain access to this server:

```json
[
    {
        "ignoresPlayerLimit": false,
        "name": "PlayerName123",
        "xuid":"1234567890123456"
    },
    {
        "ignoresPlayerLimit": false,
        "name": "AnotherPlayerName456",
        "xuid":"1234567890123457"
    }
]
```

where the `xuid` key is not strictly needed, and will be filled in when the players connect to the server.

- `data/permissions.json`: this file contains additional permissions information for the players, e.g.

```json
[
    {
        "permission": "operator",
        "xuid": "1234567890123456"
    }
]
```

- `data/server.properties`: configuration file for the server, see (here)[https://minecraft.fandom.com/wiki/Server.properties].

- `.env`: Optional file to be sourced before launching the container to name the server:

```bash
export LEVEL_NAME="<WorldName>"
```

where `<WorldName>` should be replaced with the actual world directory name. `MyWorld` is used as the world name by default.

## Starting the Server

Once configured, set the `LEVEL_NAME` variable:

```bash
# Either source the .env file
source .env

# Or export the variable directly
export LEVEL_NAME="My World Name"
```

Then run:

```bash
docker compose up -d
```

And stopping the server:

```bash
docker compose down
```
