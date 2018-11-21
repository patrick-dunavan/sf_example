# sf_example


The attached files are an example subset of the chicagocentralmsbl.com website (development site @ http://testx.chicagocentralmsbl.com) I maintain as a former member of board of directors - as well as a former player (if you review the site long enough, my picture will show up!).  I took maintenance of the site in 2004, and maintain the site upgrades, etc. in the offseason.  I often use the site to bounce ideas/concepts into the application in the early stages.


In general, attached are: 

*** The Spring (4) controller for normal http requests;  I use "DSL-like" methods/calling/shortcuts that would normally follow a catalog of global or domain-centric concepts; in the instance provided, it does not go through peer-review/acceptance  - List<String> list = safeList(as(getList(foo())) insn't fluent - but the wrappers - designed to be safe - are a time saver and eventually - I believe - make the code much more easy to follow as long as the language is expressive.

*** A service / interface / impl for retrieving data.

*** A mocked unit test against one of the services.

*** The ant build (This build relies on the underlying Eclipse-generated .classes) does not include integration into the unit test suite, code coverage, etc.  This is by design for a minimal build/deploy; Unit tests/code coverage for this project is performed by hand utilizing embedded Junit runner with eclEmma for code coverage.  less complilation is included as well as triggered during any change to the .less filein the IDE.

I am stating to note the process above is much different from a triggered compile/build/test/coverage/deploy from Jenkins, etc.  I use in a more formal environment.  


The general architecture:

*** PostgreSQL is the backend database - it houses only the current season's statistics + each season's summary statistics for each player. During any web visitor's interaction, the database is not used (other than push/contact requests initiated by the visitor - "add my infomation for the draft") - for maximum performance; for most interactions, the CPU cycles of pointing cache data into a user's request, forward/ouptut the result.  Any cache misses are due to the archives - which are not preloading.  After a season is completed, the individual team/player/season stats are removed (in deference to the season's ending XML representation).  A cahce "miss" is file-related, -> retreive the file, marshall into the corresponding java structure, save to the (files) cache, and return.

*** Uses tiles 2.x, many links use ajax calls to replace "id" zones in the page to avoid full page reloading (raw javascript / jqeury / DOM manipulation); this will slowly be replaced by most likey - reactJs.

*** Every statistic, game score, league/team schedule - regardless of the season - is stored in flat file format XML backed by (XSD-validating) Castor object mapping (when you see the code -- "_cacheFiles") during a batch operation.  This helps adjust the number of archived data stored into memory(using ehCahce) to maintain and predict requests.  The application currently does not predict which data to pre-load/cache - but the opportunity to do so exists.  The normal "twice a day batch" wall+clock time to calculate the entire season/team/player individual/lifetime stats averages 13 seconds (4 core/HT Intel Xeon cpu).

*** The current season/detailed items are stored into the "application context" in memory; (_cacheObjects);  they are backed by the flatfile interpretations, but accounting for 90%+ of the requests in the application, are pre-loaded into the cache/direct memory. 

*** The front-end was converted to mobile "friendly" in 2017; I am not a UI expert, but took a UI existing over 10 years and was able to convert it into something usable on a mobile during my "slack time" maintaning the site.  It has a long way to rework and make standard.  The CSS is slowy being converted into LESS for a more standard structure - included in the build as well as triggered / deployed locally when modified.


Off-season updates coming as time allows: 

*** 1) Convert all XML flat file data into noSQL (mongodb) to easier access/retain the data.

*** 2) Configure the xml data in mongo to the json equivelent - in order to remove the "java-mapping" equation; most of the pages currently are JSP-evaluated java structures.

*** 3) (pre-req on 1/2 above); Start the process of single/responsive page design; the process has begun with the simple reactJS flow for sponsors - maintain and continue further.




Thank you! 

Patrick Dunavan

