## Background

### Web Services

Web services enable interaction between computer systems over a network {Anonymous:bRhwymPh}. One system may call on another to provide data or a service without requiring a human user to mediate the interaction. Mobile devices have limited processing power and storage available, so off-device storage and processing empowers on-device applications.

Service Oriented Architectures (SOA) is a standard governing software design that aims to compose a software product from loosely coupled, and hence replaceable, components {Endo:2010wf}. Designers commonly employ this pattern as a method for distributed computing {Palacios:2011eo}. A set of descriptive XML documents, such as Web Services Description Language (WSDL), enable service builders to publish to service registries and then consumers to find and bind to services suited to their needs. Communication is carried out with XML-based messages based on the Simple Object Access Protocol (SOAP), another highly capable standard.

Representational State Transfer (REST) services are easy to develop and consume {Castillo:2011ve}. The adoption of RESTful services has led to an explosion of data available on the web, particularly with mobile applications in mind as end consumers.

REST services use HTTP/HTTPS as their transport layer {Castillo:2011ve}. This permits them to employ the standard HTTP response codes to indicate the success of a request. When a server is able to successfully respond to a request it sends the integer 200 along with the response headers and response body payload. The server may reject an improperly formatted request; these are the 400 series response codes. Examples include the often seen 404 code for a missing resource or 403 for failed authorisation. A server-side fault that prevents a proper response is assigned a 500 series response code, such as the catch all 500 Internal Server Error code. Less frequently seen, the 300 series codes indicate that the sought resource has been moved and the requester is directed to the new location.

It should be noted that SOAP messages may use many more transport layers than REST services {Castillo:2011ve} and as such cannot rely singularly on the HTTP response codes to indicate request failure. As a consequence, they often include error or exception details in the response body while setting the response code to the contrary 200 success value.

### Spatial Web Services

Spatial data are a computer representation of any information with a location dimension {Huisman:2009uj}. It digitally models the real world. Web services that deliver location data over a network or perform geospatial functions are spatial web services.

#### Open Geospatial Consortium Web Map Service

The Open Geospatial Consortium (OGC) is an international group of industry, government, academic and community representatives whose aim is to improve business processes through the integration of location data {Reed:2011kt}. The OGC direct their main supporting efforts towards the creation of location data and service standards and strategies.

A Web Map Service (WMS) composes an image file from server stored vector and raster layers in response to a request in a URL. The open source and standards driven approach meant that WMS was widely adopted and became a cornerstone for web mapping technology. The standard is now quite old; the documentation for version 1.3.0 was finalised in 2006 {delaBeaujardiere:2006vq}.

#### Open Geospatial Consortium Web Feature Service

A Web Feature Service (WFS) returns geographic vector data in GML (Geographic Markup Language, a derivative of XML) in response to a URL request. It is a more complex and capable service than WMS. If fully deployed, WFS grants external users full create, read, update and delete (CRUD) access to a geographic database {Vretanos:2005ut}.

The WFS standard is of a similar age to WMS. Version 1.1.0 is most commonly deployed, dating from 2005 {Vretanos:2005ut}. Version 2.0 from 2010 gained capability and complexity from GML3 and somewhat simpler use from stored queries.

#### Google Maps Engine

Google Inc.'s Google Maps Engine (GME) service enabled the creation of more sophisticated web mapping services on top of the Google Maps interface. Whereas the familiar Google Maps application only allowed one or two additional map layers to be displayed, Google Maps Engine could host many hundreds of datasets in the cloud and perform multi-layer geographic analysis {Anonymous:s3eShq99}. The full version of GME was an enterprise application and cloud service, with off-the-shelf or bespoke solutions created to suit a client's needs. The scalability and reliability of Google's service were a significant attractor to geospatial providers, such as Landgate.

From the 22nd of November 2014, Google redirected GME web site bound traffic to their Google Maps for Work service {Anonymous:A\_DLJUOY}, a more streamlined approach to providing enterprise mapping solutions.

In a commercial decision, Google Inc. announced the deprecation of the GME API on the 29th of January 2015 {Anonymous:2015tg}. Google shut the service on the 29th of January 2016.

#### Esri ArcGIS for Server and ArcGIS REST API

ArcGIS for Server is Esri's enterprise level product for intra/Internet GIS and provisioning web services {Anonymous:BHtz-GD9}.

The ArcGIS REST API exposes ArcGIS for Server data and functions as web services. This modern API has been fully developed since 2010 {Anonymous:hoTu0aor}. ArcGIS for Server's age means it is also capable of supporting older web service standards such as SOAP.

### Landgate

Landgate is the trading name of the Western Australian Land Information Authority, the statutory authority given charge of maintaining the state's land and property information system {Anonymous:2004tv}. The organisation is the inheritor of the mandate of various incarnations of the Department of Lands and Surveys, dating back to the original Survey Office in the 19th Century.

Landgate's role incorporates managing property ownership and transfer records, as well as property valuations to government agencies {Anonymous:x1iQOCOB}. Vital to society in the connected age, Landgate is Western Australia's leading spatial data agency. Landgate has successfully commercialised spatial data creation and access. Their cumulative efforts considerably lessened their dependence on funding from the state government. The success of this strategy has led to a projected 5% increase in the number of datasets served through the 2015/16 financial year {Anonymous:2015va}.

![Organisation of Landgate and WALIS](Graphics\Landgate WALIS & SLIP Org Chart.png)

The Western Australian Land Information System (WALIS) is a partnership between government agencies, the private sector, academia and the community. Their aim is to improve access to location information for the betterment of the Western Australian community {LocationInformationStrategyProgramCoordinationTeam:2012te}. The Shared Location Information Platform (SLIP) is WALIS's spatial data portal, the Western Australian government's Spatial Data Infrastructure (SDI), managed by Landgate. The portal presents datasets owned and maintained by authoritative agencies, standardises data formats and simplifies access.

SLIP Future is WALIS's programme to revamp the original SLIP Enabler portal and infrastructure {Anonymous:2014ww}. The older infrastructure was deemed incapable of handling projected usage and implementing new features. WALIS built a new platform around Google's Software as a Service (SaaS) Google Maps Engine (GME). The new environment offered significant advantages in reliability, scalability and feature set {Anonymous:2014ww}.

In January 2015, Google announced the deprecation of Google Maps Engine {SLIPFuture:2015uc}. Further, they planned to shut the service entirely by the end of January 2016 {Anonymous:2015tg}. Landgate and WALIS were left in search of a new provider for the SLIP Future programme. Esri aggressively sought the business of GME refugee organisations {Anonymous:7YAzB1Ym} offering free software replacements and membership to business partnership programs. In July 2015, Landgate selected Esri's ArcGIS Server and Portal as the replacement for GME {Anonymous:2015uc}. Web services offering datasets in Esri's ArcGIS REST APIs replaced GME's API through a transition period through the end of 2015 and beginning of 2016.

Landgate's mandate to provide spatial data services through SLIP has been somewhat derailed by the deprecation of Google Maps Engine. The work presented within looks at developing a testing suite to aid Landgate and WALIS in measuring their success against SLIP's goals. Related work, explored below, is taken as a guide to design and implementation, detailed in the Materials and Methods section.