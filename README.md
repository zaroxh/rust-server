# Rust server that runs inside a Docker container
Fork of [Didstopia/rust-server](https://github.com/Didstopia/rust-server)

This fork adds a healthcheck and more environment variables to set (see below for a full list).

## docker-compose.yml
```
services:
  rust-server:
    container_name: rust-server
    image: ghcr.io/zaroxh/rust-server:master
    restart: unless-stopped
    ports:
      - 28015:28015/tcp
      - 28015:28015/udp
      - 28016:28016/tcp
      - 28016:28016/udp
      - 28017:28017/tcp
      - 28017:28017/udp
      - 28082:28082/tcp
      - 28082:28082/udp
    volumes:
      - ./rust-server/:/steamcmd/rust
    environment:
      - RUST_SERVER_IDENTITY=rust-server
      - RUST_SERVER_NAME=[EU] Rust Server running in Docker Container
      - RUST_SERVER_DESCRIPTION=Some good server description
      - RUST_SERVER_MAXPLAYERS=50
      - RUST_SERVER_CRON_WIPE_SCHEDULE=0 19 * * 4
      - RUST_SERVER_STARTUP_ARGUMENTS=-batchmode -load -nographics -swnet +server.tags weekly,EU +server.secure 1 +wipeTimezone Europe/Berlin
      - RUST_UPDATE_CHECKING=1
      - RUST_OXIDE_ENABLED=1
      - RUST_HEARTBEAT=1
      - TZ=Europe/Berlin
```

## Environment variables
```
RUST_SERVER_STARTUP_ARGUMENTS (DEFAULT: "-batchmode -load -nographics +server.secure 1")
RUST_SERVER_CRON_WIPE_SCHEDULE (DEFAULT: "" - Cron Wipe Schedule)
RUST_SERVER_TAGS (DEFAULT: "" - Server Tags)
RUST_SERVER_IDENTITY (DEFAULT: "docker" - Mainly used for the name of the save directory)
RUST_SERVER_PORT (DEFAULT: "" - Rust server port 28015 if left blank or numeric value)
RUST_SERVER_QUERYPORT (DEFAULT: "" - Rust server query port 28016 if left blank or numeric value)
RUST_SERVER_SEED (DEFAULT: "12345" - The server map seed, must be an integer)
RUST_SERVER_WORLDSIZE (DEFAULT: "3500" - The map size, must be an integer)
RUST_SERVER_NAME (DEFAULT: "Rust Server [DOCKER]" - The publicly visible server name)
RUST_SERVER_MAXPLAYERS (DEFAULT: "500" - Maximum players on the server, must be an integer)
RUST_SERVER_DESCRIPTION (DEFAULT: "This is a Rust server running inside a Docker container!" - The publicly visible server description)
RUST_SERVER_URL (DEFAULT: "https://hub.docker.com/r/didstopia/rust-server/" - The publicly visible server website)
RUST_SERVER_BANNER_URL (DEFAULT: "" - The publicly visible server banner image URL)
RUST_SERVER_SAVE_INTERVAL (DEFAULT: "600" - Amount of seconds between automatic saves.)
RUST_RCON_WEB (DEFAULT "1" - Set to 1 or 0 to enable or disable the web-based RCON server)
RUST_RCON_PORT (DEFAULT: "28016" - RCON server port)
RUST_RCON_PASSWORD (DEFAULT: "docker" - RCON server password, please change this!)
RUST_APP_PORT (DEFAULT: "28082" - Rust+ companion app port)
RUST_BRANCH (DEFAULT: Not set - Sets the branch argument to use, eg. set to "-beta prerelease" for the prerelease branch)
RUST_UPDATE_CHECKING (DEFAULT: "0" - Set to 1 to enable fully automatic update checking, notifying players and restarting to install updates)
RUST_UPDATE_BRANCH (DEFAULT: "public" - Set to match the branch that you want to use for updating, ie. "prerelease" or "public", but do not specify arguments like "-beta")
RUST_START_MODE (DEFAULT: "0" - Determines if the server should update and then start (0), only update (1) or only start (2))
RUST_OXIDE_ENABLED (DEFAULT: "0" - Set to 1 to automatically install the latest version of Oxide)
RUST_OXIDE_UPDATE_ON_BOOT (DEFAULT: "1" - Set to 0 to disable automatic update of Oxide on boot)
RUST_RCON_SECURE_WEBSOCKET (DEFAULT: "0" - Set to 1 to enable secure websocket connections to the RCON web interface)
RUST_HEARTBEAT (DEFAULT: "0" - Set to 1 to enable the heartbeat service which will forcibly quit the server if it becomes unresponsive to queries)
```
