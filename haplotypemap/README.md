
This repo uses git submodules. Clone using the following command:

```
git clone --recurse-submodules https://github.com/laceysanderson/mycontainers4dev.git
```

To build the image run:

```
docker build -t="haplotypemap" .
```

To create a container run:

```
docker run --publish=9010:80 -tid --cap-add=NET_ADMIN --name=haplotypemap haplotypemap /usr/sbin/init
docker exec -it haplotypemap drush en haplotypembed -y
```

You can confirm the current build of the haplotype-map js app is working by going to http://localhost:9010/sites/all/libraries/haplotype-map/dist/index.html.

You can check whether it is embedding properly by going to http://localhost:9010/haplotype-map/view.

For successful embedding, the app must not change any of the surrounding Drupal site AND Drupal must not interfere with the js app.
