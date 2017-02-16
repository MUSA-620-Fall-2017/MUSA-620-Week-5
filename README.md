# MUSA-620-Week-5

Intro to Databases / NYC Taxi data with Google BigQuery


https://bigquery.cloud.google.com/welcome/bigquery-158617?pli=1

http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml

https://console.cloud.google.com/storage/browser?project=bigquery-158617

https://console.cloud.google.com/iam-admin/iam/project?project=bigquery-158617

# Assignment

This assignment is not required. You may turn it in by email (galkamaxd at gmail) or in person at class.

**Due:** by the end of class next week, 22-Feb

**Task:**

- Option 1: Using population data from the U.S. Census, color each census tract according to the number of taxi pickups normalized by population.
- Option 2: Color each NYC Census tract according to the average time it takes to get to JFK Airport by taxi.

![Distribution of NYC Taxi Pickups](https://blueshift.io/nyctaxipickups.png "Distribution of NYC Taxi Pickups")

**Deliverable:** A choropleth map, similar to the one we made in class.

- **Option 1:** For this assignment, you will need to create a "GeoID" (countyID + tractID) to join the census data to the shapefile. The shapefile posted here does not give the county code, but it does give the NYC borough, which is equivalent. You can convert between boroughs and counties using this table.

| Borough	| Borough Code | County | County Code |
|-----|------|-------|-------|
|Bronx|2|Bronx County|5|
|Brooklyn	|3	|Kings County	|47|
|Manhattan	|1	|New York County	|61|
|Queens|	4|	Queens County	|81|
|Staten Island|	5	|Richmond County	|85|

- **Option 2:** For the second assignment option, you will need to add two additional pieces to your query (see below). It must be restricted to include only taxi trips going to JFK Airport and it must return information about the trip duration.

*SELECT ROUND(Pickup_latitude, 3) AS lat, ROUND(Pickup_longitude, 3) AS lon, COUNT(*) AS num_trips,
*SUM(TIMESTAMP_TO_SEC(TIMESTAMP(tpep_dropoff_datetime)) - TIMESTAMP_TO_SEC(TIMESTAMP(tpep_pickup_datetime))) AS total_duration_in_seconds
*FROM [TaxiTrips.yellow_taxi_jun]
*WHERE Dropoff_longitude > -73.823 AND Dropoff_longitude < -73.749 AND Dropoff_latitude > 40.618 AND Dropoff_latitude < 40.667
*GROUP BY lat, lon


