# INSPIRE Good Practice: STAC as an INSPIRE Download Service

## Name of the GP
**STAC as an INSPIRE Download Service**  



## Description of the GP
This good practice presents an alternative INSPIRE predefined-access download services solution, based on the **SpatioTemporal Asset Catalog (STAC)** specification.

STAC is a modern and flexible framework, designed to organize and access large volumes of Earth observation data. STAC has since gained traction as a more general standard for handling satellite images, aerial photographs, raster data and other large datasets.

Within the framework of INSPIRE, bulk downloading has so far been implemented using **ATOM feeds**. The ATOM-based services offer a simple and standardized method for downloading files, but they have limitations in terms of scalability, discoverability and support for dynamic and complex datasets.

As an alternative to the ATOM services, **STAC could be used**. STAC provides a simple JSON-based interface for describing and indexing predefined, downloadable datasets. STAC also offers a simple solution for searching, finding and downloading datasets from the catalog. The API is RESTful and is based on the **OGC API-Features** standard. The structure of the framework and the functions that the framework offers make STAC a suitable, modern, alternative API solution for bulk downloading of INSPIRE datasets.


## INSPIRE Component(s)
This good practice covers the **INSPIRE network services** and specifically the **INSPIRE Download service**.


## References

### Normative References
- [**STAC Specification**](https://stacspec.org/en/about/stac-spec/) *- SpatioTemporal Asset Catalog Specificatoin*
- [***OGC API - Features - 1***](http://docs.opengeospatial.org/is/17-069r3/17-069r3.html "OGC API - Features - Part 1: Core") *- OGC API - Features - Part 1: Core*
- [***OGC API - Features - 2***](http://docs.opengeospatial.org/is/18-058/18-058.html "OGC API - Features - Part 2: Coordinate Reference Systems by Reference") *- OGC API - Features - Part 2: Coordinate Reference Systems by Reference*
- [***OpenAPI 3.0***](http://spec.openapis.org/oas/v3.0.3 "OpenAPI Specification 3.0") *- OpenAPI Initiative (OAI). OpenAPI Specification. The latest patch version at the time of publication of this document was 3.0.3, published in February 2020.*
- [***IRs for NS***](https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:02009R0976-20141231&from=EN "Implementing Rules for Network Services (consolidated version of 31/12/2014)") *- Commission Regulation (EC) No 976/2009 of 19 October 2009 implementing Directive 2007/2/EC of the European Parliament and of the Council as regards the Network Services*
- [***IRs for ISDSS***](https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:02010R1089-20141231&from=EN "Implementing Rules for interoperability of spatial data sets and services (consolidated version of 31/12/2014)") *- Commission Regulation (EU) No 1089/2010 of 23 November 2010 implementing Directive 2007/2/EC of the European Parliament and of the Council as regards interoperability of spatial data sets and services*
- [***INSPIRE Good Practice: Data-Service Linking Simplification***](https://github.com/INSPIRE-MIF/gp-data-service-linking-simplification/blob/main/good-practice/good-practice-fiche.md)

### Other References
Provide other references, e.g. to papers, presentations etc.
- [***Setting up an INSPIRE Download service based on the OGC API-Features standard***](https://github.com/INSPIRE-MIF/gp-ogc-api-features/blob/master/spec/oapif-inspire-download.md)
- [***Presentation STAC good practice candidate, MIG-T meeting #82***](https://wikis.ec.europa.eu/download/attachments/177046460/MIG-T82_Good%20Practice_STAC_v2.pdf?version=1&modificationDate=1757413911675&api=v2)



## Relevance & Expected Benefits
A new Good Practice describing how the SpatioTemporal Asset Catalog (STAC) specification can be used to implement INSPIRE-compliant download services for predefined datasets will lower the implementation barrier and increase the availability and thus the value of data.

While the existing INSPIRE Implementing Rules and Technical Guidelines describe how to deliver such datasets mainly through ATOM feeds or WCS, these approaches have significant limitations in terms of scalability, usability, and alignment with modern data delivery practices.

The proposed Good Practice aims to go beyond the minimum legal requirements by introducing a solution based on modern, widely adopted standards that improve user experience and operational efficiency. STAC is a lightweight, JSON/REST-based specification designed to catalogue and describe spatiotemporal assets, and it is already widely used in the Earth observation and open data domains. It supports hierarchical catalog structures, direct links to downloadable files, and spatial/temporal filtering, which makes it well suited for INSPIRE’s predefined dataset download use case.

The **Data-Service Linking Simplification** approach reduces complexity for both users and data providers. The ambition in this Good Practice is to align with the principles of Data-Service Linking Simplification, ensuring that datasets and their download services are linked together in only one place, namely in the dataset metadata. STAC Good Practice therefore will **not** address service metadata according to ISO 19115 and ISO 19119, nor the linking back to dataset metadata.

For INSPIRE implementers, this Good Practice will help to lower the technical barrier to providing bulk downloads for their data. For users, it will offer faster, more intuitive access to data in commonly used formats. In general, it will improve access, interoperability and automation of data in the INSPIRE infrastructures.


## Intended Outcome
By following the proposed good practice, data providers will be able to publish pre-defined INSPIRE datasets via a modern, STAC-based download service. This will allow users to easily discover available datasets, browse them through a clear directory structure and download complete data packages in standard formats such as GML, GeoPackage or GeoTIFF/COG.


## Evidence of Implementation & Support


## Limitations
STAC Good Practice does not cover:
- Direct access to spatial objects or dynamic datasets (covered by WFS/OGC API - Features).
- Real-time or on-demand data access.
