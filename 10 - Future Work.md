## Future Work

This work is by no means exhaustive. There remain several possibilities for expanding the application's reach and improving the depth of information generated from a campaign.

The foremost improvement to LandgateAPITest's functionality would be a more detailed investigation of the tests that failed their reference check~~, i.e. their response data did not match that stored in the web app database~~. This process could be semi-automated. Response data could be scanned for keywords such as "exception" in XML key/values to identify exception responses in place of the proper response data. ~~Partial responses could be identified by longest common string comparison functions. Analysis of these categories of failed responses could provide more accurate insight into Landgate's servers' suitability for mobile device traffic. This, in turn, would improve SLIP's mobile suitability metrics for Landgate and WALIS.~~

~~A closer collaboration with the Landgate team could permit the investigators to inspect the server logs for the web app's requests. The causes of failed requests could be discerned from a combination of the LandgateAPITest app data and the server's log data. Especially, testers could relate server error conditions and logs to requests with a 500 response.~~

~~The OASIS Web Services Quality Factors {Kim:2012wm} identify three types of latency in requests, ClientLatency, NetworkLatency and ServerLatency. Their sum being the total response time (that which LandgateAPITest records). Analysis of server logs could differentiate ServerLatency and NetworkLatency and compare latency in a variety of situations common to mobile devices.~~

~~Further development work could create a version of the LandgateAPITest mobile app suitable for Android OS devices. This would broaden the base of testers available and add another dimension to the result data. Investigation could show whether the different spatial server types offer better performance and reliability for iOS or Android devices.~~

Reference data can be considered in a more adaptable methodology than a straightforward equal/not equal test. The minor changes to GetCapabilities documents that caused their Reference Checks to fail wholesale could be averted through cleverer comparisons. Advanced string comparison techniques, such as longest common substring or edit distance, could be given a threshold similarity to assign success. For example, strings that are 90% the same could pass.

This study only compared OGC services provisioned by Landgate's earlier server infrastructure. It would be instructive to see whether Esri provisioned OGC services compared favourably with other OGC servers.

Success in collaborating with Western Australia's Landgate authority could be replicated with other Australian state cadastre authorities, such as NSW Land and Property Information. Determination of response time frequency distributions and rates of reference check failures would provide similar guidance to other organisations and offer opportunities to learn from one another which could lead to improved services for all Australian states.
