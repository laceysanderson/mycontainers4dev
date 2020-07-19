
To build the image run the following command in this directory (i.e. `jbrowse_play`).
```
$ docker build -t="jbrowse2play" .
```
This will take quite awhile -be patient!

To run the image:
```
$ docker run -itd -p 8080:80 -p 5432:5432 --name jbrowse2play jbrowseplay
```

You can now access the following locations in your browser:
 - Your Tripal Site: http://localhost:8080
 - Your JBrowse-Web Installation: http://localhost:8080/sites/all/tools/jbrowse2/index.html

## JBrowse Configuration

See the official documentation here: [Intro to the JBrowse 2 configuration](http://jbrowse.org/jb2/docs/config_basic). I recommend usage of the command-line tools (installed on this docker) as described here: [JBrowse2 Command line tools](http://jbrowse.org/jb2/docs/cli).

## JBrowse Usage

See the [official JBrowse2 user guide](http://jbrowse.org/jb2/docs/user_navigation) for information on how to use this new version of the JBrowse genome viewer.

## Container Maitentance

```
### List all the available containers.
$ docker container list

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                    NAMES
87e4334d97f9        jbrowse2play        "docker-entrypoint.s…"   26 minutes ago      Up 25 minutes       0.0.0.0:3000->3000/tcp   nervous_mclean

### See currently running containers.
$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                    NAMES
87e4334d97f9        jbrowse2play        "docker-entrypoint.s…"   25 minutes ago      Up 25 minutes       0.0.0.0:3000->3000/tcp   nervous_mclean

### Stop a container.
$ docker container stop 87e4334d97f9

### Restart a container.
$ docker container start 87e4334d97f9

### Remove all stopped containers.
$ docker container prune
```
