# Install pygeoapi

## Setup python

```bash
apt install -y python3-pip
```

```bash
python3 -V
```

```bash
pip3
```

## Run pygeoapi

git clone https://github.com/geopython/pygeoapi && cd pygeoapi

pip3 install -r requirements.txt

pip install -e .

vi example-config.yml

```yml
server:
    bind:
        host: 0.0.0.0
        port: 5000
    url: http://localhost:5000
    mimetype: application/json; charset=UTF-8
    encoding: utf-8
    language: en-US
    # cors: true
    pretty_print: true
    limit: 10
    map:
        url: https://maps.wikimedia.org/osm-intl/{z}/{x}/{y}.png
        attribution: '<a href="https://wikimediafoundation.org/wiki/Maps_Terms_of_Use">Wikimedia maps</a> | Map data &copy; <a href="https://openstreetmap.org/copyright">OpenStreetMap contributors</a>'

logging:
    level: ERROR

metadata:
    identification:
        title: pygeoapi default instance
        description: pygeoapi provides an API to geospatial data
        keywords:
            - geospatial
            - data
            - api
        keywords_type: theme
        terms_of_service: https://creativecommons.org/licenses/by/4.0/
        url: http://example.org
    license:
        name: CC-BY 4.0 license
        url: https://creativecommons.org/licenses/by/4.0/
    provider:
        name: Organization Name
        url: https://pygeoapi.io
    contact:
        name: Lastname, Firstname
        position: Position Title
        address: Mailing Address
        city: City
        stateorprovince: Administrative Area
        postalcode: Zip or Postal Code
        country: Country
        phone: +xx-xxx-xxx-xxxx
        fax: +xx-xxx-xxx-xxxx
        email: you@example.org
        url: Contact URL
        hours: Mo-Fr 08:00-17:00
        instructions: During hours of service. Off on weekends.
        role: pointOfContact

resources:
    obs:
        type: collection
        title: Observations
        description: My cool observations
        keywords:
            - observations
            - monitoring
        context:
            - datetime: https://schema.org/DateTime
            - vocab: https://example.com/vocab#
              stn_id: "vocab:stn_id"
              value: "vocab:value"
        links:
            - type: text/csv
              rel: canonical
              title: data
              href: https://github.com/mapserver/mapserver/blob/branch-7-0/msautotest/wxs/data/obs.csv
              hreflang: en-US
            - type: text/csv
              rel: alternate
              title: data
              href: https://raw.githubusercontent.com/mapserver/mapserver/branch-7-0/msautotest/wxs/data/obs.csv
              hreflang: en-US
        extents:
            spatial:
                bbox: [-180,-90,180,90]
                crs: http://www.opengis.net/def/crs/OGC/1.3/CRS84
            temporal:
                begin: 2000-10-30T18:24:39Z
                end: 2007-10-30T08:57:29Z
        providers:
            - type: feature
              name: CSV
              data: tests/data/obs.csv
              id_field: id
              geometry:
                  x_field: long
                  y_field: lat
    hello-world:
        type: process
        processor:
            name: HelloWorld
```

**Please note**
Change the `url` value accordingly to the public url of the katacoda service. How to get it?

- Click on the `+` button next to the terminal
- Select `Select port to view on Host 1`
- Enter `5000` in the form and click `Display Port`
- Copy the url in the browser and replace the value of `url` in your `example-config.yml`

```yml
# this is just an example!!! DO NOT COPY!
url: https://2886795345-frugo04.environments.katacoda.com/
```

```bash
export PYGEOAPI_CONFIG=example-config.yml 
export PYGEOAPI_OPENAPI=example-openapi.yml
pygeoapi generate-openapi-document -c $PYGEOAPI_CONFIG > $PYGEOAPI_OPENAPI
```

```bash
pygeoapi serve
```

Now we are able to open the public URL that you configured above in the config.
