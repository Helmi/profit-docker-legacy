#### profit-docker

# Docker Setup for Profit Trailer and PT-Feeder

This is a combined setup for the Crypto currency bot Profit-Trailer and its Addon PT-Feeder.

## Work in progress

Currently this is very much work in progress.

## Get it working

To get it working you need Docker compose. Edit the file `docker-compose.yml` to setup versions for both PT and PTF. Be aware that PTF currently is setup to pull beta versions only. If you want to change this you need to edit the file `pt-feeder/Dockerfile` and change the URL.

Config files need to be placed in the respective config folders. Here's the structure that docker expects to exist to save persistant data. Log files are currently not saved in persistant space.

```
./container
    /pt
        /config
        /data
    /ptf
        /config
        /database
```

place your `application.properties` file from Profit-Trailer in `./container/pt/config` - PT won't run without it. Also appsettings.json and hostsettings.json are needed for PT-Feeder. They go into the `.container/ptf/config` folder.

Run `docker-compose up` to build and start both containers. Profit-Trailer can then be reached through your browser on port 8081.