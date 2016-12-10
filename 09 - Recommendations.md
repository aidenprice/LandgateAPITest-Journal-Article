## Recommendations

Esri ArcGIS Servers can provision OGC and KML web services alongside their Esri REST services. Landgate has enabled WMS services for their Public ArcGIS MapServers, but not WFS or KML. Doing so would improve interoperability for open source apps such as QGIS at little incremental cost. Older infrastructure could then be decommissioned without reduced service to the community.

Esri JSON is not the same format as the open standard GeoJSON served by GME and OGC endpoints (note, this is not an OGC standard {Reed:2011kt}). The JSON output from Esri endpoints represents the same data as a response from an OGC or GME endpoint but is laid out differently and must be parsed into an in-memory geometry object before the two can be directly compared. Replacing GeoJSON with Esri JSON requires all applications which depend on these endpoints to adapt to the new format.

The latest version of ArcGIS Server (10.4) can supply GeoJSON in response to a `Query` request {Anonymous:3DxToBXL}. Landgate employs the previous generation ArcGIS Server, 10.3.1 for their production server infrastructure {Anonymous:81mWLEl8}.

Should older OGC servers be decommissioned Landgate could offer WFS services from their current ArcGIS servers. This would allow them to continue to offer OGC standard GML despite changes to underlying server software.

Any recommendations for improving mobile suitability metrics (response time frequency distributions and reference check percentage) would require detailed discussion between Landgate and their internal and external stakeholders. Given such, these recommendations will not be addressed in this writing.
