# sf_example


The attached files are an example subset of the chicagocentralmsbl.com website I maintain as a former member of board of directors - as well as a former player (if you review the site long enough, my picture will show up!).  I took maintenance of the site in 2004, and maintain the site upgrades, etc. in the offseason.  I often use the site to bounce ideas/concepts into the application for experimentation.


The general architecture of the site: 

*** PostgreSQL is the backend database - it houses only the current season's statistics + each season's summary statistics for each  player. During any web visitor's interaction, the database is not used (other than push/contact requests initiated by the visitor - "add my infomation for the draft") - to maintain maximum performance; for most interactions, the CPU cycles of pointing cahce data into a user's request.  Any cache misses are due to the archives - which are not preloading.  After a season is completed, the individual team/player/season stats are removed (in deference to the season's ending XML representation).

*** Every statistic, game score, league/team schedule - regardless of the season - is stored in flat file format XML backed by Castor object mapping (when you see the code -- "_cacheFiles") during a batch operation.  This helps maximize and adjust the number of archived data stored into memory(using ehCahce) to maintain and predict requests.  The application currently does not predict which data to pre-load/cache - but the opportunity to do so exists.  The normal "twice a day batch" wall+clock time to calculate the entire season/team/player individual/lifetime stats averages 13 seconds (4 core/HT Intel Xeon cpu).

*** The current season items are stored into the "application context" in memory; (_cacheObjects);  they are backed by the flatfile interpretations, but accounting for 90%+ of the requests in the application - are pre-loaded into the cache/direct memory. 

*** The front-end was converted to mobile "friendly" in 2017; I am not a UI expert, but took a UI existing over 10 years and was able to convert it into something usable on a mobile during my "slack time" maintaning the site.


2018 off-season updates coming: 

*** 1) Convert all XML flat file data into noSQL (mongodb) to easier maintain the data / retain the data w/ db backups.

*** 2) Configure the xml data in mongo to the json equivelent - in order to remove the "java-mapping" equation; most of the pages are JSP-evaluated java structures.  XML provides half the battle, but JSON/other will remove the java mapping from the equation.

*** 3) (pre-req on 1/2 above); Start the process of single/responsive page design; the process has begun with the simple reactJS flows for sponsors - maintain and continue further.


Thank you! 

Patrick Dunavan










