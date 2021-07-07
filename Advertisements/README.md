# Big Data Project

**Authors:** 
Seungheon Han, Joy Yin

## Executive Summary
   By divising a series of hypotheses, our workgroup began data exploration of a "big data" stream that included information about users who had clicked on web advertisements. We explored areas such as what variable is most correlated with whether a user clicked on an advertisement, distributions of variables, and frequency analysis. Our process required utilizing Apache Spark to process the volume of data with Cloud resources. With SparkSQL, we employed a series of joins to merge several dataframes using a common ID. Our analysis shows that Cloud solutions (i.e. parallel processing) can be effectively leveraged to conduct data exploration and analyisis of several related "big" datasets to develop conclusions.
   

## **Data**
### Data Sourcing
   - Prof. Vaisman’s Azure Blob Storage (dbfs:/mnt/course-datasets/project-data).
   - Related information can be found [here](https://dnsc6290-working-with-large-datasets.netlify.app/project.html).

### Schema
<img src=https://github.com/hshehjue/Big_Data_Management/blob/main/Advertisements/images/schema.png width=60% height=60%>

### Used Data
   * **ad_info (Rows: 5,350,670,676)** 
     - *AdID*: Identity of an ad.
     - *LocatioinID*: Ad's geo-targeting (references location for regular ads). Null for contextual ads.
     - *CategoryID*: Ad's category according to the classification model (references category).
     - *Params*: Parameters for the context ad in dictionary-like format. Null for some ads(where no parameters are available).
     - *Price*: Price for an ad.
     - *Title*: Row title text. 
       
   * **location (Rows: 58,976)**
     - *LocationID*: Identifier of the location.
     - *Level*: Level of search/impression (3 = city, 2 = region, 1 = country).
     - *RegionID*: Identifier of the search/impression region.
     - *CityID*: Identifier of the search/impression city.
     
   * **search_click (Rows: 11,023,566,785)**
     - *SearchID*: Identifier for a visitors' search event.
     - *AdID*: Identifier for an ad (see also ad description in ad_info).
     - *Position*: Position of the ad in search result page (1 - is first ad on a page starting from the top). only ads on position 1,2,6,7, and 8 are logged. 
     - *ObjectType*: Type of the ad shown to user. The options are: 1 - regular free ads added by users; 2 - highlighted regular, 3 - contextual ads.
     - *HistCTR*: Some naive history-based estimation of the click-through-rate for contextual ads, calculated when the ad is shown. non-contextual ads = Null  
     - *IsClick*: 1 if there was a click on this ad. Otherwise 0. For non-contextual ads, this field equals null. 
   
   * **search_info (Rows: 9,469,373,867)**
     - *SearchID*: Identifier of search event.
     - *SearchDate*: Date and time of the search event.
     - *UserID*: Anonymized identifier of visitors cookies.
     - *IsUserLoggedOn*: Whether user was logged on with his/her login(1) or not(0)
     - *IPID*: Anonymized identifier of visitors IP.
     - *SearchQuery*: Raw query text if it was specified while search. Null otherwise.
     - *SearchLocationID*: Identifier of the location where search was made (see also Location).
     - *SearchCategoryID*: Category filter of the search.
     - *SearchParam*: Dictionary-like structure with optional filters of the search if they were specified while search. Null otherwise.
       
## **Methods**

### Ingestion
   * Spark.read() command to acquire data from source location to intilialize cloud resources and parallel processing.

### Cleaning
   * Reformatted the tab-delimited text data files.
     - Relocating headers and separating columns.
     - Adding an index column.
   * Change the name of a column to differentiate it from the column with the same name on another table.
     - AdID (ad_info)

### Preparation
   * Employed SparkSQL to join dataframes on a common ID.
   * Converting some computation-required string values to integer or float data type.
     - IsClick
     - HistCTR
     - Price

### Tools
   * **Azure - Databricks**
     - Apache Spark
     - SparkSQL API
     - PySpark API
    
### Questions & Hypotheses
1. Which contextual advertisements were clicked by the users most?
2. Do the click records have certain relationships with the ad prices?
   - *(hypothesis 1)* the advertisements more clicked by users are more expensive. 
   - *(hypothesis 2)* the higher historical click-through-rate the ads have, the more expensive their prices.
3. What are the most Searched Ids and what are the locations of them?.=


### Visualizations
   * Bar chart of the top 10 num of click by title of the ads.
   * correlation heatmap for "Price", "number_of_click", and "CTR".
   * scatter plot for "Price" with each of the "number_of_click" and "CTR" attributes. 
   
## Challenges (technical/non-technical) & Remedies
   * When multiple dataframes are collected or taken many times, several computing stages are skipped or the commands stop running.
     - Solved by connecting the working space to a new cluster.
   * Memory usage caps when converting data structures for enhanced analysis.
   * Converting datatypes to capture appropriate visuals.
      * Solved by listing datatypes and applying appropriate conversions.
   * It is difficult to switch a location when using Azure because it may not allow you to run a cluster. 
   * The unused balance of credit will qucikly run out when you change to a larger cluster.

## Results/Conclusions
   * Advertisement for the product "Велосипед Racer Racer X61170-К Red" was clicked the most with 16,835 clicks 
   * Ad prices do not have specific relationships with both # of click and CTR

## Future Work
   * It would be useful to uncover strength of relationship between variables using statistical analysis.
   * It could be useful to further subdivide the data bypass memory constraints.
   * Check the size of the tables before working on it and start to estimate the size of cluster you will need.
   * Run some machine learning model to analyze a more specific result.


## Code Files
* [Final Product](https://github.com/hshehjue/Big_Data_Analysis/blob/main/Advertisements/BigData_Advertisement.ipynb)
