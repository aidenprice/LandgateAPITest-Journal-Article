## Conclusions

This study's contexts are in a state of nearly constant change. Web services have reduced complexity due to the dominance of REST APIs, but the number of services available has grown exponentially. Mobile devices have more processing power, larger batteries and faster connections to the internet. There are whole new categories of mobile devices, such as smartwatches, that change the mobile device landscape. Web service evaluation studies must be continually revisited just to keep pace with change.

Similarly, service providers must prepare for a changing landscape that may not even be partially realised yet. Landgate has evolved and changed direction since early in the decade to build the SLIP Future program. They must continue to adopt new technologies and processes so as to remain relevant to their customers.

This work contributes to three aspects of the body of web service evaluation literature.

Firstly, LandgateAPITest tests services from an actual mobile device in real-world mobile usage situations. Tests are therefore as close to the real mobile experience as possible. This contrasts with other academic literature that performs tests on desktop computers emulating mobile devices. This testing campaign showed that the majority of responses were received in under a second and is suitable for mobile use.

Secondly, more aspects of the interaction between client and server than merely average response time are examined. Determining the rate of inconsistent responses provides Landgate with a second metric indicative of user acceptance of SLIP's services. The campaign detailed in this work showed only 0.6% of responses returned inconsistent responses, but LandgateAPITest in its current form is incapable of determining the cause. Given the increasing frequency of reference check failures with increasing distance travelled it is assumed that the mobile network environment is the main cause.

Lastly, the examination of a single service provider, Landgate and WALIS's SLIP service, lead to practical and actionable recommendations to improve its suitability for mobile users and application developers. Google Inc.'s deprecation of Google Maps Engine and SLIP's change to Esri servers caused some disruption due to a change in JSON data format. Landgate can smooth such transitions by continuing to serve OGC data from the new Esri servers.

This is not the first work to study each of these aspects, as is evident in the related work section. It is the intersection of these three aspects that grants LandgateAPITest the opportunity to produce actionable recommendations for Landgate and provide mobile suitability metrics for objective goal success measurement.
