## Goal
The purpose of the project is to demonstrate that students can follow best practices for open scientific research in designing and implementing the project, and make their projects fully reproducible by others: from data collection to data analysis through analyzing the English Wikipedia monthly traffic from January 2008 through August 2021. The project instruction is provided [here] by the University of Washington.(https://docs.google.com/document/d/1groRZyhgOwBxlSyE4vKEhYa-khKet8iWVaVDAgOH_Y4/edit#).


## Data Description
The data consists of monthly English Wikipedia traffic data from Wikimedia Foundation from 2008-2021. The data is retrieved using two API:
- [Legacy Pagecounts](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Legacy_Pagecounts): January 2017 through July 2016; has desktop and mobile data. Mobile data doesn't start Oct 2014.
- [Pageviews](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Pageviews): July 2015 onwards; has desktop, mobile web and mobile app data
- Raw data from Legacy Pagecounts include both spider/crawler and user visitation data, while Pageviews data in the raw folder has filtered out spider/crawler traffic.
- Missing data (data without any entries from API calls) is replaced with 0.

Here is a description of the final dataset after cleaning and processing.
|Column|API|Value|Description|Mapping from the API calls|
|-|-|-|-|-|
|Year|Both|YYYY|BThis is the year of traffic data.|The first four digits of the timestamp|
|Month|Both|MM|This is the month of traffic data.|The 5-6th digits of the timestamp|
|pagecount_all_views|Legacy Pagecount API|Number of views|This is the total number of views from the Legacy Pagecount API in a month.|count from pagecount desktop + mobile|
|pagecount_desktop_views|Legacy Pagecount API|Number of views|This is the desktop traffic from the Legacy Pagecount API in a month.|count from pagecount desktop|
|pagecount_mobile_views|Legacy Pagecount API|Number of views|This is the mobile traffic from the Legacy Pagecount API in a month.|count from pagecount mobile|
|pageview_all_views|Pageview API|Number of views|This is the total number of views from the Pageview API in a month.|views from pagecount desktop + mobile app + mobile web|
|pageview_desktop_views|Pageview API|Number of views|This is the desktop traffic from the Pageview API in a month.|views from pagecount desktop|
|pageview_mobile_views|Pageview API|Number of views|This is the mobile traffic from the Pageview API in a month.|views from pagecount mobile app + mobile web|



## Known Issues

- Pageview API has the ability to filter out views from spiders/crawlers, while the Legacy Pagecounts API does not have such abilities. 
- There was about 1 year of overlapping traffic data between the two APIs, and data from both APIs in the 1 year of overlapping period is included.
- Mobile data before Oct 2014 is not available.
- 0 values were reverted back to null values when graphing to capture the essence of the missing data. The views were not actually zero, even when there was no data.
- The background of the graph was set to blank, but it can be easily changed in Matplotlib based on user preference.

## API

- API calls are modeled after this [Jupyter Notebook](https://public.paws.wmcloud.org/User:Jtmorgan/data512_a1_example.ipynb).
- [Legacy Pagecount Endpoint](https://wikimedia.org/api/rest_v1/metrics/legacy/pagecounts/aggregate/{project}/{access-site}/{granularity}/{start}/{end})
- [Pageviews Endpoint](https://wikimedia.org/api/rest_v1/metrics/pageviews/aggregate/{project}/{access}/{agent}/{granularity}/{start}/{end})

### License and Terms of Use
Documentation for the Legacy Pagecounts API can be found [here](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Legacy_Pagecounts) 
Documentation for the Pageview API can be found [here](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Pageviews) 
The license and terms of Wikimedia Foundation Rest API can be found [here](https://www.mediawiki.org/wiki/REST_API#Terms_and_conditions)
