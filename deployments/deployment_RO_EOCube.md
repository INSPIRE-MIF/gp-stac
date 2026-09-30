---
name: Deployment STAC_RO_EOCube
about: Describes a deployment of STAC RO_EOCube (ROCS / EOCube.ro) as an INSPIRE Download service.
title: "[DEPLOYMENT]"
labels: deployment
assignees: ''

---

## 1. Data provider
ROCS – Romania's Collaborative Ground Segment (COLGS-RO), West University of Timișoara (UVT), EOCube.ro platform
Website: https://eocube.ro/ , https://rocs.uvt.ro/
Funding: Ministry of Research, Innovation and Digitization, CCCDI – UEFISCDI, project PN-IV-P6-6.3-SOL-2024-2-0248, within PNCDI IV

ROCS is an open-source, cloud-native national collaborative ground segment that ingests, processes and publishes Copernicus and auxiliary data, with STAC as the catalogue backbone. It reuses EOEPCA+ and Pangeo building blocks.

## 2. Thematic scope
The catalogue (https://stac.eocube.ro) currently exposes 12 collections. They cover Copernicus data over Romania and the surrounding area, derived analysis-ready and value-added products, and a national meteorological data cube. Assets are published in cloud-native formats: COG, Zarr and GeoParquet.

* Sentinel-2 (optical)
    * Sentinel-2 Level-1C, original products (JPEG 2000), 2017-06 – present
        * https://browser.stac.eocube.ro/collections/sentinel-2-l1c
    * Sentinel-2 Level-1C converted to COG, with additional AOT, FMask and visual assets, 2017-06 – present
        * https://browser.stac.eocube.ro/collections/sentinel-2-l1c-cog
    * Sentinel-2 Level-2A surface reflectance (COG), produced in-house with Sen2Cor using a 10 m elevation model, with FMask and illumination-reliability masks, 2024-11 – present
        * https://browser.stac.eocube.ro/collections/sentinel-2-l2a
    * Sentinel-2 L2A cloudless true-colour mosaics (COG, 10 m, best-available-pixel), one item per MGRS tile and one AOI-wide item per period (EPSG:3035)
        * Monthly, 2026-01 – present: https://browser.stac.eocube.ro/collections/sentinel-2-l2a-mosaic-monthly
        * Seasonal (DJF / MAM / JJA / SON), 2026-DJF – present: https://browser.stac.eocube.ro/collections/sentinel-2-l2a-mosaic-seasonal
* Sentinel-1 (SAR)
    * Sentinel-1 Level-1 SLC, 2018-04 – present
        * https://browser.stac.eocube.ro/collections/sentinel-1-slc
    * Sentinel-1 IW radiometrically terrain-corrected (RTC) gamma0 backscatter, analysis-ready (COG, 20 m, UTM), derived from the SLC collection, 2025-12 – present
        * https://browser.stac.eocube.ro/collections/sentinel-1-rtc
* Meteorological data cube
    * ANM daily gridded meteorological data for Romania: daily maximum and minimum temperature and daily precipitation, 0.01° grid (EPSG:4326), 1961-01-01 – present, updated daily. It is published as a single analysis-ready Zarr cube and is based on the open dataset (High-Value Dataset, CC BY 4.0) of the National Meteorological Administration (ANM / MeteoRomania).
        * https://browser.stac.eocube.ro/collections/anm-daily-grids
* Elevation
    * Copernicus DEM GLO-30 (COG), global coverage
        * https://browser.stac.eocube.ro/collections/copernicus-dem-30
* Land cover
    * ESA WorldCover 2020 and 2021, 10 m (collection metadata published; items are not publicly visible at the time of writing)
        * https://browser.stac.eocube.ro/collections/esa-worldcover-2020
        * https://browser.stac.eocube.ro/collections/esa-worldcover-2021
* Burn scars
    * Burn-scar detections from a multimodal deep-learning model (TerraMind) using Sentinel-2, Sentinel-1 and elevation data. Each item holds a burn mask (COG), fire perimeters (GeoParquet) and an input manifest. Coverage runs from 2026-07 to the present, under CC BY 4.0.
        * https://browser.stac.eocube.ro/collections/sentinel-2-burn-scars-terramind-fire

Related INSPIRE data themes: Orthoimagery (Sentinel-2 L1C/L2A and mosaics), Elevation (Copernicus DEM), Land cover (ESA WorldCover), Meteorological geographical features (ANM daily grids), Natural risk zones (burn scars).

The Sentinel-1 and Sentinel-2 collections are updated continuously through automatic, event-driven ingestion; the meteorological cube is extended daily as ANM releases new data.

## 3. Envisaged use
The STAC API is in production. It is accessed through the self-hosted STAC Browser, QGIS, the platform's JupyterHub, the `eocube` CLI / Python library, and an MCP server that exposes the catalogue to LLM agents.

Access control is built into the catalogue. Every collection and item carries `eocube:owner` and `eocube:visibility`, with grants `public`, `private`, `group:ro|rw:<group>` and `user:ro|rw:<user>`. Anonymous users only see public entities. Entities a user is not allowed to see are filtered out of search results rather than refused. Authenticated users (OIDC) can publish their own collections and items through the Transaction extension.

## 4. Requirements classes
The following endpoints are implemented (from the OpenAPI definition at https://stac.eocube.ro/api):

| Method    | Endpoint                                      | Response
| --------  | --------------------------------------------- |----------------------- |
| GET       | /                                             | Landing Page (Catalog)|
| GET       | /conformance                                  | Conformance Classes    |
| GET       | /api                                          | OpenAPI definition     |
| GET       | /queryables                                   | Queryables             |
| GET       | /search                                       | Search Result (Items)  |
| POST      | /search                                       | Search Result (Items)  |
| GET       | /collections                                  | Collection List        |
| GET       | /collections/{collectionId}                   | Collection             |
| GET       | /collections/{collectionId}/queryables        | Queryables             |
| GET       | /collections/{collectionId}/items             | Item List              |
| GET       | /collections/{collectionId}/items/{itemId}    | Item                   |
| POST      | /collections                                  | Create Collection (authenticated) |
| PUT, PATCH, DELETE | /collections/{collectionId}          | Update / delete Collection (authenticated) |
| POST      | /collections/{collectionId}/items             | Create Item (authenticated) |
| POST      | /collections/{collectionId}/bulk_items        | Bulk Item creation (authenticated) |
| PUT, PATCH, DELETE | /collections/{collectionId}/items/{itemId} | Update / delete Item (authenticated) |

Declared conformance classes (https://stac.eocube.ro/conformance):

STAC API
* Core v1.0.0
* Collections v1.0.0
* OGC API – Features v1.0.0, incl. Fields, Query and Sort
* Item Search v1.0.0, incl. Fields, Query and Sort
* Item Search – Filter v1.0.0-rc.2
* Collection Search v1.0.0-rc.1, incl. Fields, Filter, Free-text, Query and Sort
* Transaction extension v1.0.0 (Collections and OGC API – Features)

OGC
* OGC API – Features – Part 1: Core, GeoJSON, OAS 3.0
* OGC API – Features – Part 3: Filter, Features Filter
* OGC API – Common – Part 2: Simple Query
* CQL2 1.0: Basic CQL2, CQL2 JSON, CQL2 Text

STAC extensions declared by collections and items: `attribution`, `authentication`, `classification`, `datacube`, `eo`, `external-ids`, `file`, `grid`, `item-assets`, `mgrs`, `processing`, `product`, `projection`, `raster`, `region`, `render`, `sar`, `sat`, `scientific`, `sentinel-2`, `storage`, `timestamps`, `version`, `view`, `web-map-links`, `xarray-assets`.

## 5. Server-side technology
* stac-fastapi-pgstac (PostgreSQL/PostGIS + pgstac) as STAC API and metadata store
    * https://github.com/stac-utils/stac-fastapi-pgstac
* Apache APISIX as API gateway and Keycloak (OIDC) for authentication, with ownership/visibility-based access control on every collection and item
* S3-compatible object storage; short-lived per-user credentials are obtained through S3 STS (`AssumeRoleWithWebIdentity`) from the OIDC token
* Serverless, event-driven processing on Kubernetes (Knative functions). Open-source services run as managed functions, e.g. TiTiler for dynamic tiles.
* Own processing services (e.g. Sen2Cor-based L2A, Sentinel-1 RTC, Sentinel-2 mosaics, burn-scar detection), which write their provenance into the `processing` extension of each item
* eocube-tools (own development, open source) is a CLI, Python library and MCP server. It ingests Sentinel-1 and Sentinel-2 granules, converts them to cloud-native formats, extracts and validates STAC metadata (xarray-compatible items) and publishes them on the user's behalf.
    * Source code: https://gitlab.dev.info.uvt.ro/rocs/tools/eocube-tools
    * Documentation: https://rocs.pages.dev.info.uvt.ro/tools/eocube-tools
    * PyPI: https://pypi.org/project/eocube/
* The catalogue is agent-ready. `eocube mcp serve` exposes the toolset over the Model Context Protocol, and a dedicated LLM agent (Qwen3) uses RAG over Qdrant to answer questions about collections, items and operations.

## 6. Endpoints and client applications
* Landing Page: https://stac.eocube.ro/
* OpenAPI definition: https://stac.eocube.ro/api (HTML: https://stac.eocube.ro/api.html)
* Self-hosted STAC Browser: https://browser.stac.eocube.ro/
* JupyterHub, with notebooks that access the catalogue through xarray / Dask: https://notebooks.svc.uvt-01.eocube.ro/
* `eocube` CLI / Python library and MCP server: `pip install "eocube[cli]"`
* QGIS: native STAC support in QGIS ≥ 3.40, or the STAC API Browser plugin, with the EOCube.ro SSO (OAuth2 / PKCE) configuration: https://rocs.pages.dev.info.uvt.ro/tools/eocube-tools/en/qgis/
* TiTiler (dynamic tiles, linked from items): https://titiler.functions.svc.uvt-01.eocube.ro/
* OIDC discovery: https://aai.eocube.ro/realms/rocs/.well-known/openid-configuration

## 7. Issues
* Many data assets are referenced with `s3://` hrefs, declared through the `storage` and `authentication` extensions, and require temporary S3 credentials obtained after an OIDC login. Only some assets have anonymous HTTPS access, such as thumbnails, the mosaic `visual` / `quality` layers and the meteorological Zarr cube. Guidance on how INSPIRE Download services should handle authenticated, S3-hosted assets and non-HTTP asset hrefs would be helpful.
* Because results are filtered by visibility, the same request can return different results for anonymous and authenticated users; for example, a collection can be listed while its items are not public. It is not clear how this should be reflected in INSPIRE metadata and in conformance testing.
* Item searches do not return `numberMatched`, which makes it harder for clients to report dataset sizes.
