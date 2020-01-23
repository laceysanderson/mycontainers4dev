
To build the image run the following command in this directory.
```
docker build -t="jbrowse2play" .
```
This will take quite awhile -be patient!

To run the image:
```
docker run --workdir /home/node/app/jbrowse-components/packages/jbrowse-web --publish=3000:3000 jbrowse2play yarn start
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
