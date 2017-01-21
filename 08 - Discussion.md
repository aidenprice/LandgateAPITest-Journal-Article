## Discussion

The results of deploying the LandgateAPITest suite to test SLIP and Landgate's spatial web services show that the mobile network environment is the major determinant of request success and response speed. Greater distance travelled during a test increases response time, whereas GET and POST requests and other server and request type dimensions have minimal affect.

The frequency distributions of response times are skewed towards shorter timeframes. Regardless of the dimension studied, for instance OGC versus Esri, XML versus JSON versus image data, the bulk of response times fell within the same order of magnitude and less than a second. The fact that the result charts need a logarithmic axis for response time to show the interquartile range indicates that Landgate's servers are suitable for the range of mobile situations investigated.

Measurement of response time is useful for determining Park and Ohm's {\*Park:2014jp} service and display quality factor. The frequency distribution of response times is an objective measurement which Landgate can use to show improvement of their service delivery.

As other studies showed, JSON responses are lighter and faster to download. They are thus better suited to mobile devices where data caps and slower mobile networks are real limitations. XML and GML suit situations where strict adherence to schema is critical to process success.

Each test type asked the same question of the three server types. The AttributeFilter test should have the same response from GME, OGC and Esri servers as the fundamental query is the same. Yet, each server type responds with differently formatted data, necessitating different referenceObjects for each. The lack of a common format makes developing applications to take advantage of services more complex. More so, the change from GeoJSON in OGC and GME endpoints to the incompatible Esri JSON requires external developers to rework their apps just to maintain existing functionality.

Esri's purely RESTful implementation denotes errors and exceptions in a manner more familiar to web and app developers. Exceptions result in a response code other than 200, namely a 400 series or 500 series integer. Whereas, OGC servers often bury exceptions within the response data itself and supply a 200 response code. Programming an application to react to a non-200 response code is much more straightforward than having to test response data for exception information.

The finding that failures are more frequent with increasing distance travelled is not an issue with Landgate's servers. Longer distances travelled during tests are an outcome of highway speed travel where the device is more likely to encounter signal interruptions or inferior signal strength.

LandgateAPITest discovered only 79 reference check failures. This is, admittedly, a small sample set from which to draw conclusions on whether spatial servers return inconsistent or incomplete data in specific circumstances. A few orders of magnitude more such errors could substantiate conclusions. Unfortunately, this would require more time and data download limit than this study has resources to allow.

According to this work, inconsistent data are delivered only 0.6% of the time. If this finding is extended, it can be assumed that there are few situations where this would be a critical hindrance for a mobile device user.

Reliable and complete response data helps ensure users can orient themselves in the map compared to their real world location, Park and Ohm's {\*Park:2014jp} perceived locational accuracy. The percentage of responses with failed reference checks is a second metric which demonstrates successful web service data delivery.

Measurements of response time frequency distribution and percentage of reference check failures are LandgateAPITest's mobile suitability metrics. Improving these metrics should lead to greater mobile map user acceptance of SLIP's services, even though they may not realise where the underlying data originates. Accordingly, greater acceptance leads to a greater intention to make use of the services. Should more users and more application developers make use of SLIP's web services Landgate could well be said to be succeeding their goal to improve access to spatial information.

The OASIS web service quality standard {Kim:2012wm} calls for calculation of Availability, Accessibility and Successability (among others). These are predicated on the assumption that the testing device is guaranteed access to the internet to perform its tests. In other words, the testing device is assumed to be infallible while the tested service is not. This is entirely possible to achieve in controlled conditions, the testing machine simply does not send a request when it is not certain of success, or ignores tests where certain preconditions of controlled experiment are not met. The output then is a percentage of tests where the tester was able to contact the service, the difference from 100% being entirely the fault of the service.

LandgateAPITest's methodology does not assume as given nor control its connection to the internet. The application proceeds with a test so long as there is some connectivity, regardless of its reliability. A failed request which timed out (and hence received a "0" response code from the iOS application) could either be the fault of server downtime or lack of a mobile network connection on the device's part.

As such LandgateAPITest is not able to reliably determine Accessibility or Availability. These are common testing metrics and future versions should address this shortcoming.

Successability is similar in that LandgateAPITest cannot reliably determine whether the lack of a response to a request is the fault of the server or the network. However, the Oasis standard assumes WSDL responses are "error-free". LandgateAPITest again does not make this assumption and interrogates the response data for errors.

Overall, LandgateAPITest is not an everyday testing suite. There are suitable applications~~, as shown in the literature review,~~ capable of determining such oft required statistics. This app more closely tests the mobile device user's experience with the data served by a geographic web service. Environmental factors of network connectivity, constrained device processing power and others have a larger effect on whether the service will successfully deliver data to meet the user's needs.

LandgateAPITest's inability to calculate Successability and related metrics is a hindrance to its deployment as the sole testing application for spatial data infrastructure. It should be deployed alongside conventional testing packages to calculate this information.
