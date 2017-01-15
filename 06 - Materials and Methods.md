## Materials and Methods

### Generalised Workflow

The mobile application user chooses to initiate a test against the Landgate servers. There are several types of test, each offers a different combination of subtests on a variety of Landgate endpoints. All subtests are enqueued and assuming that several preconditions are met the testing begins.

Testing proceeds in a cycle:

1. First, a LocationTest determines the device's latitude and longitude
2. A NetworkTest queries the device's connection to the mobile network
3. A PingTest checks the ping time to a well-known endpoint other than Landgate
4. Then the device sends one of the pre-ordered requests to Landgate's servers and captures the response data in an EndpointTest.

The cycle repeats until there are no more EndpointTests in the queue.

The client/server interaction has several failure points. It is important for this work to record failed requests as these affect a service's suitability for mobile network traffic. The device may not reach the endpoint at all due to a total lack of connectivity (recorded as response code "0") or if a EndpointTest is interrupted before its conclusion. Should the device fail to reach the server, or the server respond with a 400 or 500 code, the iOS LandgateAPITest app records the EndpointTest as a failure. These are referred to as "On Device Failures".

Note that 300 series response codes, the resource moved or redirect codes, are not considered failures. The test continues to the redirected resource where it will eventually earn a 200 success code or a failure code.

Immediately upon the test commencing, the device records the current date and time~~ as a Unix time value, the number of seconds since 00:00 on the first of January 1970~~. Similarly, when the test concludes (successfully or otherwise) the device records the current date and time again. The total response time is the difference between these two time values.

![Generalised Workflow Flowchart](Graphics\LandgateAPITest Generalised Workflow V2.png)

After all tests in the queue are complete the device stores all tests, their details and response data to a local database. The mobile app can query this database to display results to the user.

The user may choose to upload the results to the LandgateAPITest web app at a later time, ideally when the device is connected to Wi-Fi. ~~It is not desirous to immediately upload the result as it could double the data usage on the user's mobile data plan. Should an upload fail, the user may retry as many times as they wish.~~

LandgateAPITest's web application conducts the analysis on all results for each campaign of testing. When each test is successfully stored in the web app's database, it adds a task to the app's task queue. When the app has spare processing capacity, the queued task fires a request to the app to analyse the result.

In the analysis, the web app attempts to create a new Vector object to contain the results of the analysis. It requires the LocationTest, NetworkTest and PingTest results from directly before and the same from directly after each EndpointTest. Given the sequence of location, network, ping and endpoint tests each Vector shares its following three results with the next EndpointTest.

A gateway decision requires all six tests be present. Should one be missing the analysis is aborted and the result disregarded.

Otherwise, the web app proceeds to check the EndpointTest's response data against a set of reference data. These are exemplar responses to each request which are assumed to be the "true" data.

If the response received by the iOS app is identical to the reference response, then the entire test is considered successful. The iOS application may assume a test is successful given it receives a 200 response code from the Landgate server. Often though OGC servers will respond with a 200 code but send exception text in place of the response data. Tests that fail at this stage are referred to as "Reference Check Failures" and have an appropriate flag set on the record on the web application database.

During execution of the `Analyse` function, the web app records the percentage of reference check tests successful for each test type. When a test type returns less than 5% successful reference checks it is assumed that there is a process error or an incorrect reference object and disregard the test type entirely. ~~These tests are flagged False for their "ReferenceCheckValid" property to allow them to be filtered out.~~

The resultant Vector objects are the basis for all analysis and graphical representation. The web application produces pie charts of the various test categories and graphs of response time or distance travelled by category. Each graph is available from the web app's `Graph` endpoint and responds with the latest information in the database.

### Data Model and Structures

The application code draws a distinction between a Test object and a Result object. The Tests are templates and the action of performing a test. Results are concrete records of enacted tests, stored in a database and the subject of analysis.

A LocationTest is the template and the act of determining the device's location. A LocationResult is the latitude and longitude output stored on the device and uploaded to the web application.

The following subsections detail each data object as laid out in the figure below.

![LandgateAPITest Data Model Class Diagram](Graphics\LandgateAPITest Data Model Class Diagram.png)

#### TestCampaign

A unique and human-readable string identifier which groups many TestMasters into a single campaign, potentially from multiple devices. This class combines tests into a unit of work for an individual client.

~~The TestCampaign class in the web application has no properties other than its name. It serves as the ancestor key for all TestMaster, Vector and CampaignStats objects, simplifying their retrieval from the datastore. In the case of this work the test database used "test_campaign" and the production database used "production_campaign" as the test campaign names.~~

#### TestMaster

A TestMaster encapsulates all tests undertaken in a single user-initiated test. The LocationTests, NetworkTests, PingTests and EndpointTests performed from a given user test have the same TestMaster as their parent object. This allows all the various subtests to be queried with their fellows in the `Analyse` function.

~~TestMasters also group subtests according to the user's perception of the manner in which the tests were done. Thus, allowing the user to review a TestMaster and its children as a single unit of test work in the iOS app interface.~~

All TestMasters and their children inherit from the ResultObject superclass in both the web and iOS applications. In this manner, they inherit the same properties of datetime, testID, parentTestID and so forth. ~~This is for the sake of convenience and avoiding repeated code.~~

TestMasters have properties relating to the test device itself which cannot change through the cycle of subtests. The record includes the device type, the version of its operating system and a unique identifier for the device. The device ID is Apple Inc.'s "ID for vendor" a key unique to both the device and the application vendor. This key cannot be traced to a particular device without the application's signed certificate.

The database record corresponding to a TestMaster is a TestMasterResult object.

##### TestEndpoint

The primary focus of the study, TestEndpoints request a set response from the Landgate server. The TestEndpoint records the details of the template (server type, HTTP method, the URL and so forth), the test's outcome (successful or failed on the device), the start and finish time and date, and the data received in the endpoint's response.

TestEndpoints are stored in the iOS application database as EndpointResult objects. Each TestMaster will enact dozens of TestEndpoints. Consequently, each TestMasterResult will be the parent to dozens of EndpointResults.

##### LocationTest

Acquiring the mobile device's position throughout testing is key to LandgateAPITest's methodology. Information on the environment in which a given test was undertaken can be derived from this data, such as device travel distance and speed.

A LocationTest acquires a latitude and longitude value in the WGS84 coordinate reference system common to GPS devices.

The LandgateAPITest iOS app requests a 10-metre accuracy for location fixes. This accuracy is not guaranteed, should the device be unable to locate with the desired accuracy it will report what it can after timing out. As with all GPS devices, the environment affects location accuracy, particularly when testing indoors. Looser GPS accuracy saves the device's battery power which otherwise would be wasted in trying to acquire a more accurate location fix.

The web application and iOS application databases store each LocationTest's outcome as a LocationResult.

##### NetworkTest

The mobile network connection varies depending on the cell tower, its capabilities and obstacles in the intervening space.

A NetworkTest queries the iOS device for the properties of its network connection. Each NetworkTest records the mobile network provider (called carrier in mobile device parlance) and the class of the mobile network (for example, EDGE, HSDPA, LTE).

LandgateAPITest tests specifically for a Wi-Fi connection before testing for a mobile network connection.

~~NetworkTests have a property to hold a unique identifier for a cell tower. In its current form, LandgateAPITest does not record anything in this property. The iOS device reports details of its mobile network connection through Apple's Core Telephony framework. Intended for the use of mobile communication providers much of Core Telephony's functionality is private. Apps utilising such functions submitted to Apple Inc.'s App Store for review will be summarily rejected. The code LandgateAPITest uses should not be condemned under the current regime. Recording the cell tower id would be cause for rejection, however, so it is excluded.~~

The result object for a NetworkTest is a NetworkResult.

##### PingTest

As LandgateAPITest cannot directly test network connection speed, a proxy is taken in its place. A PingTest sends a HEAD request to www.google.com.au and measures the time until it receives a response. HEAD requests do not demand any data in the response body, so any intervening time is a factor of the mobile connection and processing time on the Google web server. These two factors are unfortunately inseparable given the app's limitations.

The result object stored in the database for a PingTest is a PingResult.

#### ReferenceObject

ReferenceObjects hold the correct response data from the Landgate server for each request. Server, returnType and other test template properties identify ReferenceObjects from one another and allow comparison to a TestEndpointResult. The reference property holds the response data in text, either XML, JSON or images converted to base64 text.

These exemplar responses were requested and stored on the 5th of April, 2016. This postdates GME's replacement. References for GME requests were stored in April 2016 from the first test responses in December 2015. Dynamic parts of responses were excluded from the final ReferenceObject, for example, any date or time value that changes between requests.

The administrator uploads text files containing ReferenceObject references to the web application's code repository. A request to the `StoreReferences` endpoint enqueues a task to add new and replace old ReferenceObjects with the text file contents.

#### Vector

The web application's `Analyse` function parses each TestEndpoint object and attempts to generate a new Vector object. Vectors encapsulate the LocationTest, NetworkTest and PingTest immediately preceding the TestEndpoint along with those immediately following it, retaining pointers to these objects. The function determines the change in Location, Network conditions and Ping response time and takes them as a proxy for the mobile device's changing connectivity environment through the EndpointTest.

The logic to retrieve the six related subtests from the datastore is as follows;

1. Query only those records specific to the subtest type (LocationTests, NetworkTests or PingTests)
2. Retrieve only results with the same TestMaster key as the TestEndpoint
3. Filter results to only those with a datetime property less than the TestEndpoint's datetime for the three preceding subtests (or greater than for the three following tests)
4. Sort the results by their datetime, descending for preceding subtests and ascending for following subtests
5. Return only the first result, that being the closest in time to the TestEndpoint

If any one of the six subtests is absent, the Vector object cannot be reliably created and the process is aborted. The TestEndpoint is marked "IMPOSSIBLE" to prevent any further automated attempts at analysis. Such objects are not considered any further in this study. Situations like this may arise where the device cancelled a test partway through, precluding the three following tests.

The Haversine distance formula gives a great circle distance travelled between two LocationTests (essentially a straight line at these scales). Dividing this result by the time difference gives an average speed in metres per second. The time between two LocationTests is not the same as the TestEndpoint's total elapsed time. The interval is greater as it allows for NetworkTests, PingTests and the duration of the LocationTests themselves.

The generation of the mobile network is here taken as a proxy for connection speed. For example, LTE is a fourth-generation network and assigned 4.0 for a networkClass property, where HSDPA would be assigned 3.5, CDMA 2.5 and so on. Wi-Fi is approximated to generation 5.0 due to its higher potential connection speed. Subtracting the following networkClass from the preceding one gives a networkChange value. Positive values reflect improving network generation and negative values degrading.

The change in response time for a HEAD request to google.com.au before and after an EndpointTest is another proxy for change in network connection speed. Subtracting the following test's response time from the preceding test's response time gives a positive pingChange value for improving network speed and a negative one for degrading speed.

The `Analyse` function also performs the reference check. It assigns the Vector's referenceCheckSuccess property a True value if the TestEndpoint's response data contains the ReferenceObject's reference text or False otherwise.

Vector objects are the basis for all further analysis in this study. All graphs in this work show the Vector rather than the original TestEndpoint or its subtests.

~~#### CampaignStats

The CampaignStats class stores counts of TestEndpoints and other subtests, enabling calculation of descriptive statistics for a particular TestCampaign. CampaignStats updates when the iOS application uploads a new TestMaster to the database, adding new counts onto existing values. Also, when the `Analyse` function creates a new Vector object it updates the CampaignStats properties for reference check success.

The overwhelming majority of CampaignStats properties concern the percentage of successful reference object checks. 0% reference check success rates will exclude the entire test type from further consideration. See the Results section.~~

### iOS Mobile Application

~~#### Mobile Application Design Principles~~

The LandgateAPITest iOS application should be quick to build and simple to maintain. The app's design eschews user interface flair in favour of basic views, such as the ubiquitous UITableView. This has the beneficial side-effect of making the app familiar and easy to use for a broader range of the community.

~~Where possible, open source libraries should replace handwritten code. There being no point to reinventing functionality already well developed and freely available. A common pattern in modern app development, community supported libraries fill narrowly focussed functions. These are easily incorporated into an iOS project through dependency management applications and community code repositories such as GitHub.~~

~~LandgateAPITest is not a privacy focussed app. The application collects data that many would consider intrusive, such as location or mobile network connection details. Without this information, the application would not fulfil its objectives. The app's help text encourages users who find such invasiveness unacceptable to uninstall the application.~~

~~The application is also a heavy user of the device's battery and mobile network downloads. These are similarly unavoidable, being core to the application's function. The help text highlights that users may upload a test while on a Wi-Fi network to avoid data charges for uploading a TestEndpoint's response data.~~

~~Given these two points, users could be justly concerned that the application would be a noticeable drain on their battery and data plan. LandgateAPITest addresses this issue by only testing when the application is in the device's foreground, meaning on the screen while the device is awake. Should the application be sent to the background, it immediately enters an abort state, cancelling active tests and storing what results it has to the database. This can be triggered by the user selecting a different app, clicking the Home button, or by an interrupting phone call.~~

~~#### iOS Application Architecture~~

~~Apple Inc. advocates the Model-View-Controller (MVC) design pattern in object-oriented code. A controller class intermediates all interaction between the data model layer and the views on the device screen. LandgateAPITest follows this pattern by implementing viewcontroller classes for each screen presented to the user.~~

![Typical Model-View-Controller (MVC) design pattern](Graphics\Mobile Application Architecture-01.png)

~~The majority of the application's logic does not reside in viewcontrollers however. It is a common problem in MVC pattern design that the controller classes amass logic to the point of becoming unwieldy and difficult to maintain. LandgateAPITest's viewcontrollers call upon the SingletonTestManager and SingletonUploader classes when the user initiates a test or an upload to the LandgateAPITest web app respectively. These act as an interface for the model layer, abstracting model logic from the point of view of the viewcontrollers.~~

![LandgateAPITest's modified MVC design pattern incorporating singleton, state-machine controller classes as a model management layer](Graphics\Mobile Application Architecture-02.png)

Firing requests at Landgate's endpoints concurrently, rather than synchronously, would give unreliable response time results. An analysis would not be able to determine what proportion of response time was a factor of the device resolving multiple threads of computation. To avoid this complication LandgateAPITest's iOS app uses a state machine architecture.

![State machine UML diagram](Graphics\LandgateAPITest Mobile Application State Diagram.png)

The state machine completes functions sequentially. The completion of each test fires an event function causing the application to change state and after that perform different functions.

When the user initiates a test the SingletonTestManager class switches to its prepareForTest state where it checks preconditions and creates a TestMaster object. From there the SingletonTestManager enters a loop; testing location, network, ping time to google.com.au and then testing a Landgate endpoint (a TestEndpoint) and back to location. The loop continues until the TestMaster's queue of TestEndpoints is exhausted, after which the device writes the TestMaster and all its subtests to its database. Each state performs distinct actions and does not interfere with tests preceding or following as none may start until the earlier test has successfully finished.

At any time the state machine may abort the loop if the preconditions are not met, the app leaves the foreground, or the battery is exhausted. It immediately skips to the post-test state and attempts to save the test results gathered to the device database. Any test (endpoint, location, network or ping) cancelled part-way through is aborted and marked as "Failed On Device."

~~Uploading in the background of the application uses a similar pattern. The SingletonUploader class changes state from "Ready" to "Uploading" and thence to "Success" or "Failure" depending on the response code from the web app. It settles back to the "Ready" state once its upload queue is emptied.~~

~~#### Swift Open Source Packages~~

~~##### Realm Mobile Database~~

~~The Realm open source mobile database {realmrealmcocoa:2016vs} is a much simpler on-device storage solution than the proprietary Apple Inc solution. LandgateAPITest stores all test results in a Realm database file.~~

~~##### Transporter State Machine~~

~~Denis Telezhkin's Transporter library {DenHeadlessTranspor:2016ta} offers a straightforward state machine implemented in Swift, available under the MIT licence. LandgateAPITest relies upon Transporter state machines for the SingletonTestManager and SingletonTestUploader classes.~~

~~##### Reachability~~

~~Ashley Mill's Reachability library queries the device to determine whether and how it is connected to a network {ashleymillsReachabi:2015to}. LandgateAPITest depends on Reachability's response in two areas. Firstly, having a network connection is a prerequisite to starting a test, either through Wi-Fi or 2G, 3G or 4G mobile network. Secondly, the iOS standard telephony libraries report a mobile network connection regardless of whether there may be an overriding Wi-Fi network connection. LandgateAPITest checks Reachability beforehand for a Wi-Fi connection.~~

~~##### KDCircularProgress~~

~~Kaan Dedeoglu's KDCircularProgress library initiates a progress indicator that fulfils a circular ring as the task approaches completion {kaandedeogluKDCircu:2015vt}. LandgateAPITest uses KDCircularProgress to show the percent completion of a test, updating the indicator each time a sub-test calls its completion delegate method. The library was chosen as it aligned with the design aesthetic of recent iOS releases.~~

### Google Apps Engine Web Service

~~#### Web Service Design Principles~~

The ideal for any web service is to present the latest available data to requesters. LandgateAPITest presents statistics, maps and analysis on objects in the datastore at request time. End users need not await final reports but can check on the status of a testing campaign whenever they wish.

The iOS testing app can produce a large set of testing data in a short timeframe. Cloud computing power is capable of scaling to accommodate excess load, but at a cost. The web application acts to smooth out high load by deferring computationally intensive tasks to avoid peak load and minimise cost.

The web application should analyse TestEndpoint results and not just represent them. Generating actionable information from pure data has much more value to the end user. Similar applications produce appealing graphs with little scientific merit. LandgateAPITest's charts, while less visually gripping, offer in-depth analysis and proper scientific methodology.

~~#### Python Application Architecture~~

~~Google App Engine (GAE) Python applications derive their basic functionality from the webapp2 open source library {Welcometowebapp:2011vk}. Developers define web app endpoints and map them to Python classes, so landgateapitest.appspot.com/database maps to the Database class in Python code. Then the HTTP method maps to functions within that class. A POST request to the `Database` endpoint fires the Database class's post() function adding the request body to the database. A GET request calls the get() function and downloads a TestMaster record to the requester.~~

~~Python functions may call for a task to be enqueued. The GAE system will fire the specified request at a later time, ideally when processor load is minimal. A successful POST request to the `Database` endpoint queues an `Analyse` endpoint GET request as one of its last tasks. Similar tasks which are anticipated to consume more than trivial resources are deferred as queued tasks in LandgateAPITest, such as importing reference text files to the datastore or updating the model schema.~~

~~Google App Engine applications may use any of Google Inc.'s several cloud data storage solutions. LandgateAPITest uses Google Cloud Datastore, a NoSQL database quite distinct from relational databases in that it does not store all records as atomic rows in tables, rather as schema-less objects in distributed documents.~~

~~#### Python Open Source Packages~~

~~##### Matplotlib~~

~~Well known in academia, Matplotlib is an open source Python library capable of producing detailed graphs from complex datasets {matplotlibmatplotli:2016vd}. LandgateAPITest's web app leveraged Matplotlib to build graphs of up to the minute Vector object data queried from Google's Cloud Store. Programmatically compiling the figures in this report allows them to be recreated on demand with the latest information from testers.~~

~~Matplotlib's analytical power is enhanced when paired with Numpy {NumPyNumpy:2016vy}. A mathematically focussed library, most useful in LandgateAPITest for its arrays, which are much more analytically oriented than generic Python list collections.~~

~~##### Leaflet~~

~~The LandgateAPITest web application offers a heatmap of test locations. More precisely, the map shows each Vector object's LocationTest prior to the EndpointTest. Leaflet {Agafonkin:2016wz} is a lightweight JavaScript mapping library, it is ideal for a simple application such as this.~~

~~Visualising 16,000 test locations as generic markers would result in a confusing map. The Leaflet.heat {Agafonkin:2015ww} library generalises multiple points into a single heat map layer. Closely clustered tests are represented by warmer colours, dispersed ones by cooler colours. OpenStreetMap tiles comprise the base map, available under a CC BY-SA open licence and built by the community of OpenStreetMap contributors.~~

~~### Other Applications Deployed~~

~~Besides code incorporated directly into the product applications, several other applications were instrumental to app development.~~

~~#### Paw~~

~~Keeping track of 46 REST requests, each with minor variations from its neighbours, required more than a handwritten list. Paw (version 2.3.3) {Anonymous:tn} is a Mac application designed for testing REST requests. It simplifies the process of composing the request and its query components. Its most helpful feature is its Swift NSURLSession code output, suitable for directly pasting into an iOS application repository. The code in LandgateAPITest's EndpointTester class where it fires a request to the Landgate server is derived from Paw's example code.~~

~~#### Atom~~

~~Atom (version 1.7.2) {atomio:vz} is Github Inc's open source text editor used primarily for LandgateAPITest's Python web app development. The Github community has built a plethora of extensions expanding the application's capabilities far beyond the average plain text editor. This entire report was draughted in MarkDown styled plain text in Atom.~~

~~#### Xcode~~

~~Apple Inc's Xcode Integrated Development Environment (IDE) {Anonymous:3QN3N1hm} is the orthodox application for developing apps for Apple machines. LandgateAPITest's iOS app was entirely built in Xcode version 7.3.~~
