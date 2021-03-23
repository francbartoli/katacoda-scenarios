# Prepare a tileset

## Create Mapbox Vector Tiles via tippecanoe

```bash
git clone https://github.com/mapbox/tippecanoe.git && cd tippecanoe
```

docker build -t tippecanoe:latest .

cd ../pygeoapi/
docker run -it --rm \
    -v ${PWD}:/data \
    tippecanoe:latest \
    tippecanoe --output-to-directory=/data/tests/data/tiles1/ --force --maximum-zoom=11 --drop-densest-as-needed --extend-zooms-if-still-dropping --no-tile-compression /data/tests/data/ne_110m_lakes.geojson


```bash
ls -lart tests/data/tiles1/
```

```bash
docker run -d -p 9000:9000 --rm --name pygeoapi-minio \
   --user $(id -u):$(id -g) \
   -e "MINIO_ACCESS_KEY=pygeoapi" \
   -e "MINIO_SECRET_KEY=pygeoapi" \
   -v ${PWD}/tests/data/tiles:/data \
   minio/minio server /data
```

Let's open the minio console in the browser:

- Click on the `+` button next to the terminal
- Select `Select port to view on Host 1`
- Enter `9000` in the form and click `Display Port
- Enter `pygeoapi/pygeoapi` to login

You are seeing the MVT directories' structure!!
