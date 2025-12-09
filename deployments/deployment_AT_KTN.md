---
name: Deployment STAC_AT_KTN
about: Describes a deployment of STAC AT_KTN as an INSPIRE Download service.
title: "[DEPLOYMENT]"
labels: deployment
assignees: ''

---

## 1. Data provider
Kärntner Geographisches Informationssystem (KAGIS), Regional Government of Carinthia, Land Kärnten
Website: https://kagis.ktn.gv.at/
Email: kagis@ktn.gv.at

## 2. Thematic scope
* Airborne Laser Scanning (ALS)
    * Digital Elevation Model & Digital Surface Model (GEOTIFF)
        * https://gis.ktn.gv.at/kagisbrowser/#/collections/KAGIS_coll_ALS1
        * https://gis.ktn.gv.at/kagisbrowser/#/collections/KAGIS_coll_ALS2_raster_gailtaleralpen
        * https://gis.ktn.gv.at/kagisbrowser/#/collections/KAGIS_coll_ALS2_raster_hohetauern
        * https://gis.ktn.gv.at/kagisbrowser/#/collections/KAGIS_coll_ALS2_raster_kreuzeckgruppe
    * Point Cloud Data (COPC)
        * https://gis.ktn.gv.at/kagisbrowser/#/collections/KAGIS_coll_ALS2_pc_gailtaleralpen
        * https://gis.ktn.gv.at/kagisbrowser/#/collections/KAGIS_coll_ALS2_pc_hohetauern
        * https://gis.ktn.gv.at/kagisbrowser/#/collections/KAGIS_coll_ALS2_pc_kreuzeckgruppe
* Orthoimagery
    * State-wide aerial surveys (COG & GEOTIFF)
        * https://gis.ktn.gv.at/kagisbrowser/#/collections/KAGIS_coll_ortho_klagenfurt_2022460
        * https://gis.ktn.gv.at/kagisbrowser/#/collections/KAGIS_coll_ortho_osttirol_2021160
        * https://gis.ktn.gv.at/kagisbrowser/#/collections/KAGIS_coll_ortho_tamsweg_2021360
        * https://gis.ktn.gv.at/kagisbrowser/#/collections/KAGIS_coll_ortho_villach_2022160
        * https://gis.ktn.gv.at/kagisbrowser/#/collections/KAGIS_coll_ortho_wolfsberg_2022360
        * https://gis.ktn.gv.at/kagisbrowser/#/collections/KAGIS_coll_ortho_zell_am_see_2022650
        * https://gis.ktn.gv.at/kagisbrowser/#/collections/KAGIS_coll_ortho_zeltweg_2022260
    * Local drone aerial surveys (COG)
        * https://gis.ktn.gv.at/kagisbrowser/#/collections/KAGIS_coll_fluege_akl

## 3. Envisaged use
STAC API is in production (in use with STAC Browser and QGIS Plugin)

## 4. Requirements classes
The following endpoints based on the req classes are implemented:

| Method    | Endpoint                                      | Response
| --------  | --------------------------------------------- |----------------------- |
| GET       | /                                             | Landing Page (Catalog)|
| GET       | /conformance                                  | Conformance Classes    |
| GET       | /search                                       | Search Result (Items)  |
| POST      | /search                                       | Search Result (Items)  |
| GET       | /collections                                  | Collection List        |
| GET       | /collections/{collectionId}                   | Collection             |
| GET       | /collections/{collectionId}/items             | Item List              |
| GET       | /collections/{collectionId}/items/{itemId}    | Item                   |

## 5. Server-side technology
* PostGIS primary metadata database
* Apache Solr as secondary metadata data storage
    + STAC data generation + Ingestion into Solr node: https://github.com/gis-code-share/stac-dynamic-generation
* Python FastAPI
    + In-House API implementation: https://github.com/gis-code-share/stac-solr-fastapi

## 6. Endpoints and client applications
* Landing Page: https://gis.ktn.gv.at/api/stac/v1
* Self-hosted STAC browser: https://gis.ktn.gv.at/kagisbrowser/
* QGIS Plugin: https://plugins.qgis.org/plugins/qgis_stac/

## 7. Issues
* Link to other GitHub issues, or describe here issues that you encounter with the guidelines for the use of STAC as an INSPIRE Download service.
