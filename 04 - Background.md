## Background

### Web Services

Web services enable interaction between computer systems over a network {Anonymous:bRhwymPh}. One system may call on another to provide data or a service without requiring a human user to mediate the interaction. Mobile devices have limited processing power and storage available, so off-device storage and processing empowers on-device applications.

Service Oriented Architectures (SOA) is a principle of software design that aims to compose a software product from loosely coupled, and hence replaceable, components {Endo:2010wf}. Designers commonly employ this pattern as a method for distributed computing {Palacios:2011eo}. 

Representational State Transfer (REST) services are easy to develop and consume {Castillo:2011ve}. The adoption of RESTful services has led to an explosion of data available on the web, particularly with mobile applications in mind as end consumers.

REST services use HTTP/HTTPS as their transport layer {Castillo:2011ve}. This permits them to employ the standard HTTP response codes to indicate the success of a request. When a server is able to successfully respond to a request it sends the integer 200 along with the response headers and response body payload. The server may reject an improperly formatted request; these are the 400 series response codes. 300 series codes indicate that the sought resource has been moved and the requester is directed to the new location.

### Spatial Web Services

#### Open Geospatial Consortium Web Map Service

The Open Geospatial Consortium (OGC) is an international group of industry, government, academic and community representatives whose aim is to improve business processes through the integration of location data {Reed:2011kt}. 

A Web Map Service (WMS) composes an image file from  The standard is now quite old; the documentation for version 1.3.0 was finalised in 2006 {delaBeaujardiere:2006vq}.

#### Open Geospatial Consortium Web Feature Service

A Web Feature Service (WFS) returns geographic vector data in GML (Geographic Markup Language, a derivative of XML) in response to a  request. It is a more complex and capable service than WMS. If fully deployed, WFS grants external users full create, read, update and delete (CRUD) access to a geographic database {Vretanos:2005ut}.

The WFS standard is of a similar age to WMS. Version 1.1.0 is most commonly deployed, dating from 2005 {Vretanos:2005ut}. 

#### Google Maps Engine

Google Inc.'s Google Maps Engine (GME) service enabled the creation of more sophisticated web mapping services on top of the Google Maps interface. Whereas the familiar Google Maps application only allowed one or two additional map layers to be displayed, Google Maps Engine could host many hundreds of datasets in the cloud and perform multi-layer geographic analysis {Anonymous:s3eShq99}. The full version of GME was an enterprise application and cloud service, with off-the-shelf or bespoke solutions created to suit a client's needs. The scalability and reliability of Google's service were a significant attractor to geospatial providers, such as Landgate.

From the 22nd of November 2014, Google redirected traffic bound for the GME web site to their Google Maps for Work service {Anonymous:A\_DLJUOY}, a more streamlined approach to providing enterprise mapping solutions.

In a commercial decision, Google Inc. announced the deprecation of the GME API on the 29th of January 2015 {Anonymous:2015tg}. Google shut the service on the 29th of January 2016.

#### Esri ArcGIS for Server and ArcGIS REST API

ArcGIS for Server is Esri's enterprise level product for intra/Internet GIS and provisioning web services {Anonymous:BHtz-GD9}.

The ArcGIS REST API exposes ArcGIS for Server data and functions as web services. This modern API has been fully developed since 2010 {Anonymous:hoTu0aor}. ArcGIS for Server's age means it is also capable of supporting older web service standards such as SOAP.

### Landgate

Landgate is the trading name of the Western Australian Land Information Authority, the statutory authority given charge of maintaining the state's land and property information system {Anonymous:2004tv}. The organisation is the inheritor of the mandate of various incarnations of the Department of Lands and Surveys, dating back to the original Survey Office in the 19th Century.

Landgate's role incorporates managing property ownership and transfer records, as well as property valuations to government agencies {Anonymous:x1iQOCOB}. 

![Organisation of Landgate and WALIS](Graphics\Landgate WALIS & SLIP Org Chart.png)

The Western Australian Land Information System (WALIS) is a partnership between government agencies, the private sector, academia and the community. Their aim is to improve access to location information for the betterment of the Western Australian community {LocationInformationStrategyProgramCoordinationTeam:2012te}. 

The Shared Location Information Platform (SLIP) is WALIS's spatial data portal, the Western Australian government's Spatial Data Infrastructure (SDI), managed by Landgate. The portal presents datasets owned and maintained by authoritative agencies, standardises data formats and simplifies access.

SLIP Future is WALIS's programme to revamp the original SLIP Enabler portal and infrastructure {Anonymous:2014ww}. The older infrastructure was deemed incapable of handling projected usage. WALIS built a new platform around Google's Software as a Service (SaaS) Google Maps Engine (GME). The new environment offered significant advantages in reliability, scalability and feature set {Anonymous:2014ww}.

In January 2015, Google announced the deprecation of Google Maps Engine {SLIPFuture:2015uc}. Further, they planned to shut the service entirely by the end of January 2016 {Anonymous:2015tg}. Landgate and WALIS were left in search of a new provider for the SLIP Future programme. Esri aggressively sought the business of GME refugee organisations {Anonymous:7YAzB1Ym} offering free software replacements and membership to business partnership programs. In July 2015, Landgate selected Esri's ArcGIS Server and Portal as the replacement for GME {Anonymous:2015uc}. Web services offering datasets in Esri's ArcGIS REST APIs replaced GME's API through a transition period through the end of 2015 and beginning of 2016.

Landgate's mandate to provide spatial data services through SLIP has been somewhat derailed by the deprecation of Google Maps Engine. The work presented within looks at developing a testing suite to aid Landgate and WALIS in measuring their success against SLIP's goals. Related work, explored below, is taken as a guide to design and implementation, detailed in the Materials and Methods section.
