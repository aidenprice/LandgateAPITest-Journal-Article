## Abstract

Landgate is Western Australia's premier spatial data provider. The Shared Location Information Platform (SLIP) is the WA Government's spatial data portal.

Research on spatial web service testing aims to test under controlled conditions, to eliminate variables of network connectivity or device speed. Controls tend to poorly reflect real world mobile device usage. This research eschews controls, preferring to gather data on the test environment at test time.

Further, research tends to focus on response time as the main metric of service performance, an objective measure. Few papers consider whether the data returned are correct. Mobile downloads can be interrupted by lost signal, resulting in an incomplete response. Unreliable responses decreases a user's desire to reuse and recommend a mapping application.

LandgateAPITest is a suite composed of a mobile application for testing and a Google App Engine web application for storage and analysis. The suite combines response time measurements with inconsistent responses to paint a picture of Landgate's servers' suitability for mobile devices.

Deploying LandgateAPITest against SLIP's spatial web services confirms earlier studies’ findings and demonstrates that the mobile network is the biggest factor in performance and response quality.

The end result is a set of mobile suitability metrics. The frequency distribution of response time across a number of web service request types demonstrates performance. The percentage of requests with inconsistent response data measures quality.

Providing these metrics to the SLIP team will aid Landgate in objectively measuring progress towards their goal of enabling access to location information.
