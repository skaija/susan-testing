---
title: Address lookup
---

Address lookup that is also called as reverse geocoding, means finding address for given coordinates.

## Reverse geocoding endpoint

Endpoint root is available at:
> http://<i></i>api.digitransit.fi/geocoding/v1/reverse

## Supported url parameters:

| Parameter       | Type           | Description                                              |
|-----------------|----------------|----------------------------------------------------------|
| point.lat              | floating point number         | Latitude value
| point.lon              | floating point number         | Longitude value
| boundary.circle.radius | floating point number         | Search only inside given circle
| size                   | integer                       | Limit the number of results returned
| layers                 | comma-delimited string array  | Filter results by layer (value can be address, venue or street)
| sources                | comma-delimited string array  | Filter results by source (value can be oa, osm or nlsfi)
| boundary.country       | <a href="https://en.wikipedia.org/wiki/ISO_3166-1" target="\_blank">ISO-3166 alpha-2 or alpha-3</a> | Filter by country

**Note: Parameter api_key is not in use in digitransit** 

## Response fields:

| Name       | Type           | Description                                              |
|-----------------|----------------|----------------------------------------------------------|
| id           | string         | 
| gid            | string            | Global id
| layer   | string          | 
| source | string         | 
| source_id            | string         | 
| name            | string         |
| postalcode            | number         |
| postalcode_gid            | string         |
| confidence            | number         |
| distance            | number         |
| accuracy            | string         |
| country            | string         |
| country_gid            | string         |
| country_a            | string         |
| region             | string         |
| region_gid            | string         |
| localadmin            | string         |
| localadmin_gid            | string         |
| locality            | string         |
| locality_gid            | string         |
| neighbourhood            | string         |
| neighbourhood_gid            | string         |
| label            | string         |
| bbox            | string         |

### Example to get address for given coordinates (cURL)

```
curl "http://api.digitransit.fi/geocoding/v1/reverse?point.lat=60.199284&point.lon=24.940540&size=1"
```

### Example to get address for given coordinates (Browser)

http://api.digitransit.fi/geocoding/v1/reverse?point.lat=60.199284&point.lon=24.940540&size=1

### Language preference

http://api.digitransit.fi/geocoding/v1/reverse?point.lat=60.195&point.lon=24.93&lang=sv&size=1

Note, that part of the provided geocoding data does not include Swedish names, and part of the data
does not specify the language at all. A swedish-speaking person may add a new address entry
'Fabriksgatan xx, Helsingfors' to OpenStreetMap without specifying the language.
Address lookup always searches across all documents and returns found items in the preferred
language if such a language-bound name version is available, otherwise using the default name,
which in reality can represent any language. Most default names are of course in Finnish.
