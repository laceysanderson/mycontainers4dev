
To build the image run the following command in this directory (i.e. `jbrowse_play`).
```
docker build -t="jbrowse2play" .
```
This will take quite awhile -be patient!

To run the image:
```
docker run --workdir /home/node/app/jbrowse-components/packages/jbrowse-web --publish=3000:3000 -v `pwd`/public:/home/node/app/jbrowse-components/packages/jbrowse-web/public jbrowse2play yarn start
```

This should provide the following output:
```
yarn run v1.21.1
$ rescripts --max-http-header-size=100000 start
ℹ ｢wds｣: Project is running at http://172.17.0.3/
ℹ ｢wds｣: webpack output is served from /
ℹ ｢wds｣: Content not from webpack is served from /home/node/app/jbrowse-components/packages/jbrowse-web/public
ℹ ｢wds｣: 404s will fallback to /index.html
Starting the development server...

Compiled successfully!

You can now view @gmod/jbrowse-web in the browser.

  Local:            http://localhost:3000/
  On Your Network:  http://172.17.0.3:3000/

Note that the development build is not optimized.
To create a production build, use npm run build.
```

Once you see this full message, navigate to http://localhost:3000 in your browser.

The tracks are served from `jbrowse_play/public` and configuration is in `jbrowse_play/public/test_data/config.json`. While I do not know of an automatic way to add tracks, you can do so modifying the `config.json` using other tracks as a template. Just be sure to use correct JSON syntax!

NOTE: Since a) the container public directory is mounted to your local machine and b) we are running jbrowse-web in development mode, any changes you make in your local public directory are immeditely reflected at http://localhost:3000 in your browser.

Other container maitentance commands:
```
# List all the available containers.
docker container list

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                    NAMES
87e4334d97f9        jbrowse2play        "docker-entrypoint.s…"   26 minutes ago      Up 25 minutes       0.0.0.0:3000->3000/tcp   nervous_mclean

# See currently running containers.
docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                    NAMES
87e4334d97f9        jbrowse2play        "docker-entrypoint.s…"   25 minutes ago      Up 25 minutes       0.0.0.0:3000->3000/tcp   nervous_mclean

# Stop a container.
docker container stop 87e4334d97f9

# Restart a container.
docker container start 87e4334d97f9

# Remove all stopped containers.
docker container prune.
```
