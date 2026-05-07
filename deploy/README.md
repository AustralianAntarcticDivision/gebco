# General Bathymetric Chart of the Oceans Data

Data originall accessed from the
[GEBCO website](https://www.gebco.net/data_and_products/gridded_bathymetry_data/).

GEBCO's gridded bathymetric data set, is a global terrain model for ocean and land, providing elevation data, in meters, on a 15 arc-second interval grid. It is accompanied by a Type Identifier (TID) Grid that gives information on the types of source data that the GEBCO_2024 Grid is based on.

This release includes a version of the grid with under-ice topography/bathymetry information for Greenland and Antarctica.

Find out information about [terms of use and attribution here](https://www.gebco.net/data_and_products/gridded_bathymetry_data/#a1).

Documentation on [data preparation is accessible here](https://github.com/AustralianAntarcticDivision/gebco).

## Access data

### Stream data

The cloud optimised geotiff can be used directly in QGIS or
other applications using this URL:
`https://data.source.coop/ausantarctic/gebco/GEBCO_<year>.tif`.

### Example to load as Xarray

```python
from odc.stac import load
from pystac import Item

# Bounding box around Tasmania
bbox = [140.0, -45.0, 150.0, -35.0]

# Get the item as a PySTAC Item
item = Item.from_file(
    "https://data.source.coop/ausantarctic/gebco/GEBCO_2024.stac-item.json"
)

# Load using odc.stac.load
data = load(
    [item],
    bbox=bbox,
    chunks={"latitude": 1024, "longitude": 1024},
)

# Plot an interactive map
data.elevation.odc.explore(vmin=-3000, vmax=3000, cmap="terrain")
```

### Downloading

While the idea of cloud native data formats is to not download, you can
download this data using the following URLs:

* 2024: `https://data.source.coop/ausantarctic/gebco/GEBCO_2024.tif`
* 2025: `https://data.source.coop/ausantarctic/gebco/GEBCO_2025.tif`
* 2026: `https://data.source.coop/ausantarctic/gebco/GEBCO_2026.tif`
