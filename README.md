# General Bathymetric Chart of the Oceans Data

This repo holds scripts and docs for the Source.Coop GEBCO dataset.

## Documentation

The folder called `deploy` is the one that we sync to Source Coop.

Synchronise using the AWS CLI. First get credentials from Source.Coop, export them
and then run the below command to sync.

``` bash
aws s3 sync ./deploy s3://us-west-2.opendata.source.coop/ausantarctic/gebco/ --dryrun
```

## Get and convert data

```
wget https://dap.ceda.ac.uk/bodc/gebco/global/gebco_2026/ice_surface_elevation/netcdf/GEBCO_2026.zip?download=1 \
 -O GEBCO_2026.zip

unzip GEBCO_2026.zip

gdal_translate GEBCO_2026.nc out.vrt

gdal_translate out.vrt GEBCO_2026.tif \
    -a_srs "EPSG:4326" \
    -of COG \
    -co OVERVIEW_RESAMPLING=AVERAGE -co BLOCKSIZE=512 -co COMPRESS=DEFLATE -co PREDICTOR=2 -co BIGTIFF=YES -co OVERVIEW_COUNT=7

```

## Create a STAC Item

Change values as appropriate, install `rasterio` and `rio-stac`, then run the command
to create the STAC Item. Manually format, so it's not on a single line.

``` bash
rio stac \
    --datetime "2026-01-01T00:00:00.000Z" \
    --collection "gebco" \
    --asset-name "gebco" \
    --asset-href "https://data.source.coop/ausantarctic/gebco/GEBCO_2026.tif" \
    --with-proj \
    --with-raster \
    deploy/GEBCO_2026.tif > deploy/GEBCO_2026.stac-item.json
```
