
To build the image run the following command in this directory (i.e. `jbrowse_play`).
```
$ docker build -t="jbrowse2play" .
```
This will take quite awhile -be patient!

To run the image:
```
$ docker run --workdir /home/node/app/jbrowse-components/packages/jbrowse-web --publish=3000:3000 -v `pwd`/public:/home/node/app/jbrowse-components/packages/jbrowse-web/public jbrowse2play yarn start
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

## JBrowse Usage

See the following tutorials which are still in development:
- [Add a new genome to the display](https://github.com/GMOD/jbrowse-components/blob/master/docs/tutorials/empty-view.md)
- [Structural Variant Inspector; circular view](https://github.com/GMOD/jbrowse-components/blob/master/docs/tutorials/structural-variant-inspector.md)
- [Linear Genome View](https://github.com/GMOD/jbrowse-components/blob/master/docs/tutorials/linear-genome.md)

## JBrowse Config

The following examples should be modified to suit your needs. They should be added to the `jbrowse_play/public/test_data/config.json` file.

### Add a new Genome/Dataset

Add the following within the "datasets" array at the top.
```json
{
  "name": "Lens culinaris (v2.0; CDC Redberry)",
  "assembly": {
    "name": "Lc2.RBY",
    "aliases": [
      "Lc2.RBY"
    ],
    "sequence": {
      "type": "ReferenceSequenceTrack",
      "trackId": "Lc2.RBY",
      "adapter": {
        "type": "BgzipFastaAdapter",
        "fastaLocation": {
          "uri": "http://localhost:3000/Lc2.RBY/Lens_culinaris_2.0.fasta.gz"
        },
        "faiLocation": {
          "uri": "http://localhost:3000/Lc2.RBY/Lens_culinaris_2.0.fasta.gz.fai"
        },
        "gziLocation": {
          "uri": "http://localhost:3000/Lc2.RBY/Lens_culinaris_2.0.fasta.gz.gzi"
        }
      },
      "rendering": {
        "type": "DivSequenceRenderer"
      }
    }
  },
  "tracks": []
},
```

### Add a new track

Add track stanza's to the tracks array depending on the type of file you want to serve. Make sure the "trackId" is unique! You can find examples for the various types of files and track types in the `jbrowse_play/test_data/config*.json` files. Pay special attention to the track "type" which will give an indication of whether it's for the linear or circular views.

Current file types with example tracks:
 - fasta
 - bam
 - cram
 - vcf

All files must be indexed and are served directly (no processing). As such you can provide web-accessible URLs rather then local ones if they are available.

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
