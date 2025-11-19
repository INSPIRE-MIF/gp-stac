# STAC Implementation, Lantmäteriet, Sweden
## 1. Data provider

* Lantmäteriet, Sweden



## 2. Thematic scope

Digital elevation model (DEM): The DEM has national coverage of Sweden and is continuously updated using LIDAR data and from aerial photographs through stereo photogrammetry.

Orthophoto: National coverage of Sweden, updated annually with new imagery. Images are organized by acquisition year and geographic area. Images range from the most recent aerial surveys back to the 1940s.

## 3. Envisaged use

The APIs were launched for public use in february 2025.



## 4. Requirements classes

STAC Specification - SpatioTemporal Asset Catalog Specificatoin
OpenAPI 3.0 - OpenAPI Initiative (OAI).


OGC

- CQL2 - Basic Cql2 1.0
- CQL2 - Cql2 Json 1.0
- CQL2 - Cql2 Text 1.0
- OGC API - Features - Part 1 - Core 1.0
- OGC API - Features - Part 1 - Geojson 1.0
- OGC API - Features - Part 1 - Oas30 1.0
- OGC API - Features - Part 3 - Features Filter 1.0
- OGC API - Features - Part 3 - Filter 1.0

STAC

- Item Search - Filter v1.0.0-rc.2
- Collections v1.0.0
- Core v1.0.0
- Item Search v1.0.0
- Item Search - Fields v1.0.0
- Item Search - Query v1.0.0
- Item Search - Sort v1.0.0
- Ogcapi Features v1.0.0
- Ogcapi Features - Fields v1.0.0
- Ogcapi Features - Query v1.0.0
- Ogcapi Features - Sort v1.0.0

## 5. Server-side technology

Stac-utils/stac-fastapi , a python library for building a STAC-compliant FastAPI application.

The backend used is stac-fastapi-pgstac



Documentation: https://stac-utils.github.io/stac-fastapi/

Source Code: https://github.com/stac-utils/stac-fastapi



## 6. Endpoints and client applications

Digital elevation model (DEM)

https://api.lantmateriet.se/stac-hojd/v1/

Encoding: GeoJSON and COG (Cloud-optimized GeoTIFF)

Status: In production (authentication required for data asset downloads)

Orthophoto

https://api.lantmateriet.se/stac-bild/v1/

Encoding: GeoJSON and COG (Cloud-optimized GeoTIFF)

Status: In production (authentication required for data asset downloads)


## 7. Issues
General mapping principle
1. Our suggestion is to map the INSPIRE concept Spatial dataset  to the STAC representation STAC collection. However, i.e. in our (Lantmäteriet) implementation of ortophoto, the STAC collections together forms the corresponding INSPIRE dataset. The single collection is only a part of the dataset. Is the mapping principle dataset=STAC Collection still ok?
