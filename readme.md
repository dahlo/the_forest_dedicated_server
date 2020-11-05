# The Forest Dedicated Server

## First time setup
Make the changes you want to `config.cfg`, like server name and password, then copy it to where the server will look for it. There is an error in the docker image that will set the wrong permissions on the folders, but we can get around that by creating the folders manually. Setting the ownership of the server folders to UID 99 and GID 100 since those are the UID and GID of the steam user inside the container.

```bash
# get the repo
git clone https://github.com/dahlo/the_forest_dedicated_server.git
cd the_forest_dedicated_server

# create the folders
mkdir -p serverdata/serverfiles/config/
mkdir serverdata/steamcmd

# copy the config and set ownership
cp config.cfg serverdata/serverfiles/config/
sudo chown -R 99:100 serverdata
```

## Starting the server
Once you have modified and copied `config.cfg` it's time to start the server. It's as easy as typing:

```bash
docker-compose up -d
```

As long as you have port forwarding configured correctly it should start the server and it should show up in the `Dedicated (internet)` server list in the game client.

## Debugging
If it for some reason doesn't work, you can check the logs of the container with

```bash
docker-compose logs -f
```

There will be loads of serious looking error messages printed during startup, but as long as it reaches the `Game autosave started` message it should be good to go.
