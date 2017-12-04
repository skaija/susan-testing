---
title: Points of interest
---

## Vector maps 

Vector maps are available in [Mapbox Vector Tile format](https://github.com/mapbox/vector-tile-spec)

## Vector tiles

Vector tiles are available from endpoint:
<pre>https://digitransit-prod-cdn-origin.azureedge.net/:source}/:z/:x/:y.pbf</pre>

## Supported url parameters

| Parameter     | Type           | Description                                              |
|---------------|----------------|----------------------------------------------------------|
| source        | string         | one of: 'hsl-stop-map', 'hsl-parkandride-map', 'waltti-stop-map' 'finland-stop-map'
| z             | int            | Zoom level
| x             | int            | x-coordinate
| y             | int            | y-coordinate
| size          | string         | '@2x' for retina tiles or empty value for normal

## examples

> https://digitransit-prod-cdn-origin.azureedge.net/hsl-stop-map/16/37308/18959.pbf

> https://digitransit-prod-cdn-origin.azureedge.net/map/v1/hsl-stop-map/index.json