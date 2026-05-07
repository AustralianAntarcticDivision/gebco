# General Bathymetric Chart of the Oceans Data

This repo holds scripts and docs for the Source.Coop GEBCO dataset.

## Documentation

The folder called `deploy` is the one that we sync to Source Coop.

Synchronise using the AWS CLI. First get credentials from Source.Coop, export them
and then run the below command to sync.

``` bash
aws s3 sync ./deploy s3://us-west-2.opendata.source.coop/ausantarctic/gebco/ --dryrun
```

## Create a STAC Item

Change values as appropriate, install `rasterio` and `rio-stac`, then run the command
to create the STAC Item. Manually format, so it's not on a single line.

``` bash
rio stac \
    --datetime "2025-01-01T00:00:00.000Z" \
    --collection "gebco" \
    --asset-name "gebco" \
    --asset-href "https://data.source.coop/ausantarctic/gebco/GEBCO_2025.tif" \
    --with-proj \
    --with-raster \
    deploy/GEBCO_2025.tif > deploy/GEBCO_2025.stac-item.json
```
