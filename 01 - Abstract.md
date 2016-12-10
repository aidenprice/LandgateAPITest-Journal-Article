## Abstract

Landgate is Western Australia's premier spatial data provider, the lead organisation and partner of the West Australian Land Information System (WALIS). The Shared Location Information Platform (SLIP) is the WA Government's spatial data portal and the implementation of WALIS's programme to improve access to location information. Previously dependent upon Google Map Engine spatial server infrastructure, Landgate and SLIP had to pivot rapidly to Esri spatial servers to avoid loss of service due to GME's decommissioning.

Academic writing on spatial web service testing naturally aims to test under controlled conditions, to eliminate variables of network connectivity or device speed. Controls tend to poorly reflect real world mobile device usage. This research eschews controls for the greater part, preferring to gather data on the test environment at test time.

Further, academia tends to focus on response time as the main metric of service performance, an objective measure. Few papers consider whether the data returned are correct. Mobile downloads can be interrupted by lost signal, resulting in an incomplete response. Unreliable or inconsistent response data decreases a user's desire to reuse and recommend a mapping application. Were such a situation to occur repeatedly fewer application developers would employ SLIP's services in their mobile applications and fewer end users would access Western Australia's spatial information.

LandgateAPITest is a testing suite composed of an iOS application for frontline mobile device testing and a Google App Engine web application for storage, analysis and presentation of charted results. The suite combines response time measurements with errors in responses to paint a broader picture of Landgate's servers' suitability for mobile devices.

Deploying LandgateAPITest against SLIP's GME, OGC and Esri spatial web service endpoints confirms the findings of earlier studies and finds that the mobile network is the biggest factor in performance and quality of responses.

The end result is a set of mobile suitability metrics. The frequency distribution of response time across a number of web service request types demonstrates performance. The percentage of requests with inconsistent response data compared to a reference measures quality.

Providing these metrics to the SLIP team will aid Landgate and WALIS in objectively measuring progress towards their goal of enabling access to location information.
