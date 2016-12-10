## Literature Review

### Related Work

Web services are widely studied {Tahir:2013jd, Qiu:2015eq, ElIoiniNabil:2015us}. However, the scope of applications for web services is broad. There are, therefore, few studies that examine the intersection of geographic web service performance, mobile device context and a single, state-level spatial data infrastructure. Following are a cross-section of papers with aims partially aligned to those of this work.

Hamas, Saad and Abed {\*Hamad:2010tr} compared the performance of SOAP and REST APIs on mobile devices. The measured criteria were response time and transmission size which predictably favoured REST interfaces.

Their experiment design emulated a mobile device on a desktop computer; further, they restricted the simulated mobile network speed. These are useful controls in an experiment designed with a very clear aim of finding which service is faster. Real world complications such as heavy network traffic or poor signal are not addressed as a factor in the outcome. As an example, SOAP's WS-ReliableMessaging protocol may reduce overall transfer time in areas with weak signal by minimising the number of failed message attempts.

Tian et al. {\*Tian:2004cb} designed a server-client system that could optionally compress responses to save the client's download limit or skip compression when the server is under heavy load to minimise timed out requests. Working in the pre-smartphone era the team simulated an iPAQ Pocket PC, emulating the device on a Pentium III laptop. The laptop emulating the client was connected to the server via Wi-Fi, Bluetooth or a simulated mobile network. To simulate the increased latency and slower connection speed of a GPRS network, they introduced another server that throttled network speed by artificially delaying messages.

Davis, Kimo and Duarte-Figueiredo {\*Davis:2009hf} focussed on OGC Web Map Service (WMS) optimisation for mobile devices. They elaborated a service that combined the multi-layer composition of WMS with the mobile device response speed of AJAX-based web maps such as Google Maps.

Their experiment implemented the proposed service and interacted with it from a custom application deployed on a Nokia N95. Given the focus on minimising data sent and received from the device, the results vindicated their hypothesis. Unfortunately, the team declined to study response time results due to "severe fluctuations" that they attributed to an overcrowded network. They concluded, by extension not experiment, that smaller volumes of transmitted data would result in faster map interaction overall.

Fowler, Hameseder and Peterson {\*Fowler:2012bn} built a custom iPhone application to test the performance of SOAP and REST versions of a public transportation web service in Hamburg over a typical working day. They measured response time, data serialisation/deserialisation time and response size on the device itself and returned the results to their own web service. Simple and detailed messages of significantly different response size controlled whether response time was dependent upon message size. The results, as is common, were given as mean and standard deviation, descriptive statistics without discussion of error responses.

Fowler, Hameseder and Peterson's {\*Fowler:2012bn} methodology called for the mobile user to remain "fixed" while requesting and receiving the response. This is interpreted to mean stationary, contrary behaviour for mobile device use. There are countless situations in which a mobile user would be active and moving while concurrently requesting data from a web service.

Provisioning web services from a mobile device faces similar network and device limitations as consuming a service from a mobile device. Nguyen, Jørstad and van Thanh {\*Nguyen:2008jt} explored web service performance on an emulated mobile device. While investigating the influence of varied simulated mobile network speeds, they concluded that testing on an actual device would provide ideal settings for their network simulation. Indeed, the subsequent experiment showed considerable differences between emulated and real network speed influence on web service performance. Even after modifying their simulated network speed to approximate real world network speed the difference was significant.

Hussain, Wang and Toure {\*Hussain:2014ce} tested the response time and throughput of a variety of real world web services over DSL, Wi-Fi and LAN internet connections. Results were simplified to descriptive statistics, average, minimum and maximum response time. They discussed some tests with unusually long response times and speculated that it may be due to other web traffic. The specific time or other conditions of these particular tests were not elucidated. In fact, the methodology is not sufficiently detailed to provide all the parameters used in web service requests. Repeating their experiments would likely produce different results.

Yang, Cao and Evans {\*Yang:2013ff} demonstrated that WMS servers struggle with heavy loads of simultaneous requests. They recorded response times to 1, 5, 10. 30, 50 and 100 concurrent requests to six important WMS servers. They found that response times increased with the number of requests until many servers either blocked all incoming requests to handle the load or simply timed out. They made several recommendations, particularly regarding parallel requests and processing. Most helpful to this study, a simple progress bar to indicate to a user that their request is still being processed.

Recent work by Cannata, Antonovic and Molinari {\*Cannata:2014dp} load tested the transalpine HELIDEM project's OGC web services. They measured response time as they programmatically overloaded the GeoServer system using the Locust open source Python testing library.

Tantalisingly, Cannata, Antonovic and Molinari {\*Cannata:2014dp} mentioned that Locust is capable of reporting testing tasks as failed even if the server returns a 200 "Success" response code with an exception in the response data. Unfortunately, they did not go on to explain this capability, nor did their testing uncover any exceptions which Locust could have revealed to them.

The emergence of RESTful web services engendered many studies comparing performance to entrenched SOAP services {Castillo:2011ve, Kanagasundaram:2012wv}. By focussing on response performance, few experimental designs take advantage of SOAP's inherent advantages, i.e. a message layer and orchestrated distributed computing. Such a design would allow SOAP APIs to be compared more favourably with REST APIs.

Castillo et al. {\*Castillo:2011ve} compared REST and SOAP service implementations as the intermediary messaging layer for a genetic algorithm and a fitness evaluator. They also presented one of the few papers to elaborate the advantages of the older SOAP API standard against a REST API, but their experiment did not build on this. Their proof of concept methodology introduced a useful control, requests via SOAP and REST sent strings of either 100 or 1,000 characters. The proportional time difference between large and small requests controlled whether the response time depends upon the amount of data sent and received, illuminating how much response time overhead is due to the API employed.

Like other researchers, Castillo et al. {\*Castillo:2011ve} related the results of their performance tests as average response time with a margin of error. They discussed accuracy, but this concerned their genetic algorithm's accuracy, not the error rate of the web service API.

Kanagasundaram et al. {\*Kanagasundaram:2012wv} exposed an ersatz student database as a resource and performed Create, Read, Update Delete operations over SOAP and REST web services. The comparison of response time between different operations lead the team to propose a hybrid SOAP and REST web service that incorporated the security and reliability aspects of SOAP with REST APIs' ease of development.

The experiment design placed the client and server processes on separate cores of a single processor. This worked well as an experimental control but came at the expense of measuring real world performance. Furthermore, the results obtained by Kanagasundaram et al. {\*Kanagasundaram:2012wv} were averaged response times from experiments repeated until they achieved a 95% confidence level. However, not all were presented in the paper, only a select subset. Presumably, messages resulting in errors were excluded from the averaged results.

Expedients such as simulated mobile networks or emulated mobile devices can be more easily understood when considered in the context of testing a production server. Stress testing and automated test case generation, for example, both benefit from a quantity of tests unachievable with a few handheld devices. Services such as Load Impact {Anonymous:0z5u-mT-} emulate thousands of mobile users on a variety of devices with a range of network connectivity.

Mobile application testing is a rapidly growing field. Gao et al. {\*Gao:2014fp} identified four classes of mobile application testing approaches. Emulation-based testing, as seen above, where a device simulator runs on a desktop computer, is commonplace as emulators ship with most app development environments. Device-based testing runs the application and its services on a range of real devices to find edge case failures. Cloud testing suits large-scale tests scalable to requirements. Crowd-based testing employs volunteers or contractors to test apps and can reach reasonable scales; they noted that tests may not be thorough.

Yan et al. {\*Yan:2012uf} built a cloud testing suite, an approach they called Web Service - Testing-as-a-Service (WS-TaaS). Their experiment showed that cloud tested web services were capable of responding to significantly more requests than one tested from a single desktop computer. They concluded it was most likely due to the limited bandwidth and processing power of the single testing node.

### Web Service Quality and Discovery

Automated web service discovery aims to support semantic web development {Palacios:2011eo, DMello:2010hi}. An application should be able to bind a web service without supervision from the end user. How then, though, should the application choose which web service to employ from the multitude available, also without requiring user intervention. The investigators below discuss systematically and automatically applied quality metrics as a basis for deciding which web services should be bound.

Palacios, Garcia-Banjul and Tuya {\*Palacios:2011eo} surveyed Service Oriented Architecture literature to find articles focussed on dynamic binding. 57% of the 33 articles detected faults in web services and thereby excluded non-responsive services.

Orion, Marco and French {\*Oriol:2014kq} reviewed the state of the art in quality of service models for web services, surveying 65 papers written between 2001 and 2012. They showed that most researchers were assessing web services quality regarding availability (essentially the probability a request will receive a response) with 94% of surveyed papers defining the metric. Response time was second place at 83% coverage and accuracy third with 62%.

Wu et al. {\*Wu:2011kk} proposed web service registries evaluate the quality of services they expose. Service downtime, mismatches between catalogued metadata and current capability or inconsistencies when registered in multiple catalogues could lead to the selection of a suboptimal web mapping service. The catalogue service periodically interrogated an OGC WMS testing all operations listed in its GetCapabilities document. Successful tests decreased the frequency of future tests while a lack of response increased the frequency.

Wu et al. {\*Wu:2011kk} modelled quality factors using a hierarchical tree, proposed by Hanwu Zhang, one of the authors in their Ph.D. dissertation from 2008 (reference not found in English translation). This is a helpful concept for automated quality analysis as branches in the hierarchy can be weighted differently, emphasising categories of metrics (the "leaves") over others. Unfortunately, Wu et al.'s automated analysis stopped after comparing the most recent response time to a weighted average of previously recorded response times. They went on to assess map data quality through a survey method. A GUI program presented returned data to an expert user for assessment and scoring out of five on a series of quality metrics.

Miao, Shi and Cao {\*Miao:2011dh} built upon the adaptable testing frequency method of Wu et al. {\*Wu:2011kk} by halving test intervals when the response time was greater than the average of earlier tests. They went further to parameterise the proportion of failed requests. Their process was explained well in a flow chart, omitted from many similar papers.

Miao, Shi and Cao {\*Miao:2011dh} developed a C based program to crawl 100 WMS servers to measure their performance and stability as per their procedure. The paper referenced here omitted a table listing the servers assessed. As with Wu et al. {\*Wu:2011kk}, the team left data quality assessment to a survey of expert users.

### Web Service Evaluation

The OASIS Web Services Quality Factors {Kim:2012wm} defined six quality factors with 28 sub-categories.

    1.    Business Value Quality - the value arising from using a web service as compared to the cost.
    2.    Service Level Measurement Quality - the service responsiveness from a client's point of view, including time and success criteria.
    3.    Interoperability Quality - the degree to which a service conforms to appropriate standards.
    4.    Business Processing Quality - the service's reliability for business use considering transmission integrity and integration with other processes.
    5.    Manageability Quality - management processes to ensure web service quality.
    6.    Security Quality - the service's ability to prevent intrusion, interception or destruction of the service itself or its messages.

Taken all together these represent all factors that affect a client's decision to consume a web service.

The scope of this study is limited to those aspects of Landgate's service that affect their suitability for use on mobile devices. The business process and value, management, interoperability and security factors cannot be tested with a mobile device. These are more suited to desktop studies and surveys of existing clients.

Only Service Level Measurement Quality is within the purview of this study. Its sub-categories include:

    1.    Response Time - the time interval between the transmission of a request and the receipt of a response. The total time is composed of the time taken for the client to compose the request and decompose the response plus the network transmission time to and from the server plus the time taken for the server to process the request and formulate a response.
    2.    Maximum Throughput - the maximum number of requests a service can reliably respond to in a unit of time.
    3.    Availability - the proportion of time the server is operational, the complement of service downtime per measured time.
    4.    Accessibility - the probability of the web service can be reached when the system is operational, quantified as the number of received acknowledgement messages divided by the total number of requests.
    5.    Successability - the probability of receiving a successful response to a web service request, the number of responses divided by the number of requests.

This research proposes to track these factors through a series of frequent but irregularly timed tests from a mobile device deployed in situations common to the mobile network milieu.

### Acceptance

Park and Ohm {\*Park:2014jp} surveyed mobile map users to construct a technology acceptance model to investigate users' acceptance of mobile mapping applications. The research question sought to understand what factors influenced user's intention to use such mapping applications. They found two main determinants of users' attitude towards a mobile mapping service and thence their intention to make use of the service. Those being; perceived locational accuracy and service and display quality.

Park and Ohm {\*Park:2014jp} defined perceived locational accuracy as how well users envision their location in the map, essentially the degree to which mapped features correspond with a user's mental model of the world and where they are in it. This study considers that requests for map data that fail due to errors or return mismatching or incomplete data are a direct hindrance to user acceptance. A mobile map application that featured missing map tiles or incomplete geographic feature data prevents a user from determining their location in the map with respect to their real world situation.

Park and Ohm's {\*Park:2014jp} definition of service and display quality is an extension of earlier general definitions of service quality; "the degree of general performance of an information system and related services." As discussed above, quality as measurable in the context of this work includes response time and likelihood of request success.

A LandgateAPITest suite campaign, explained in the following section, produces mobile suitability metrics aligned with both factors as its outputs.
