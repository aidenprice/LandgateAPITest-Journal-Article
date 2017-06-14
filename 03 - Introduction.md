## Introduction

Landgate is Western Australia's cadastre authority and foremost spatial data agency. It is the leading organisation in the Western Australian Land Information System (WALIS) and its open data portal; the Shared Location Information Platform (SLIP). As SLIP was built on Google Maps Engine (GME), Google Inc.'s closure of the service forced Landgate and WALIS into a period of rapid change. Esri ArcGIS for Server infrastructure replaced GME as Landgate's production spatial servers.

In this work, a testing suite was built consisting of a mobile application for testing and a web service for analysis, named LandgateAPITest. The suite was applied to Landgate's spatial server infrastructure before and after the pivot away from GME.

The use of a mobile device as a test platform and its deployment in real world conditions is a departure from much of the academic research on spatial web service testing. LandgateAPITest eschews experimental controls as found in related works, such as mobile devices simulated on desktop computer hardware. Further, most research reports results as a few descriptive statistics of web service request response time. LandgateAPITest aims to inspect response data for returns inconsistent with reference data sets.

The testing suite provides a measurement set as its outputs, frequency distributions of response time and a percentage of responses with inconsistent data, termed mobile suitability metrics. These are aligned with a technology acceptance model related in other works such that improvement in these scores should occasion greater user acceptance of SLIP's spatial web services. This work, looks to uncover practical and actionable recommendations which can aid Landgate in improving their service to the community.
