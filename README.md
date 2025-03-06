# NAV-Taxi-Assignment

## ***Big Data Inspection - NYC Taxi Trips Project***

This project involves analyzing a dataset containing taxi trip information. The data includes trip details such as pickup and dropoff locations, timestamps, passenger counts, trip distances, and more. Below is an overview of the dataset, its fields, and the steps taken to analyze it.


## Dataset Overview

The dataset consists of **14,776,615 rows** of trip data covering the period from **2013-01-01 00:00:00** to **2013-02-01 10:33:08**. The data includes information such as taxi medallion, vendor ID, pickup/dropoff timestamps, passenger count, trip distance, and geographic coordinates.

### Dataset Fields

The dataset contains the following fields:

| **Field Name**            | **Description**                                       |
|---------------------------|-------------------------------------------------------|
| `medallion`                | Unique identifier for the taxi medallion.             |
| `hack_license`             | Unique license for the taxi.                          |
| `vendor_id`                | ID of the taxi vendor.                                |
| `rate_code`                | Code indicating the rate category for the trip.       |
| `store_and_fwd_flag`       | Flag indicating if the trip data was stored and forwarded. |
| `pickup_datetime`          | Datetime when the trip started.                       |
| `dropoff_datetime`         | Datetime when the trip ended.                         |
| `passenger_count`          | Number of passengers in the taxi.                     |
| `trip_time_in_secs`        | Trip duration in seconds.                             |
| `trip_distance`            | Trip distance in miles.                               |
| `pickup_longitude`         | Longitude of pickup location.                         |
| `pickup_latitude`          | Latitude of pickup location.                          |
| `dropoff_longitude`        | Longitude of dropoff location.                        |
| `dropoff_latitude`         | Latitude of dropoff location.                         |

### Data Types

Below are the recommended MySQL data types for each field:

| **Field Name**            | **Suggested MySQL Data Type**                           |
|---------------------------|---------------------------------------------------------|
| `medallion`                | VARCHAR(32)                                              |
| `hack_license`             | VARCHAR(32)                                              |
| `vendor_id`                | VARCHAR(3)                                               |
| `rate_code`                | INT(2)                                                   |
| `store_and_fwd_flag`       | CHAR(1)                                                  |
| `pickup_datetime`          | DATETIME                                                 |
| `dropoff_datetime`         | DATETIME                                                 |
| `passenger_count`          | INT(2)                                                   |
| `trip_time_in_secs`        | INT(6)                                                   |
| `trip_distance`            | DECIMAL(5,2)                                             |
| `pickup_longitude`         | DECIMAL(9,6)                                             |
| `pickup_latitude`          | DECIMAL(9,6)                                             |
| `dropoff_longitude`        | DECIMAL(9,6)                                             |
| `dropoff_latitude`         | DECIMAL(9,6)                                             |

## Geographic Bounds

The geographic coordinates are bounded as follows:

- **Pickup Latitude**: 40.400002 to 41.019676
- **Pickup Longitude**: -74.398537 to -72.050003
- **Dropoff Latitude**: 40.75 to 41.0
- **Dropoff Longitude**: -74.499222 to -72.050003

This data can be plotted on a map for visualization.

## Analysis Results

<img src="image1.jpeg" alt="1">

## **Map of Pickup and Dropoff Locations**

This map shows pickup and dropoff locations for taxi trips.
The markers on the map highlight geographic locations where taxi activity is concentrated.
Key Locations Observed:
New York City (center of most trips).
New Jersey and surrounding areas.

A few outliers on Long Island and other distant locations, indicating some long-distance trips.
Insights:
The data shows most taxi activity is centered around NYC.
Some trips extend to the suburbs and even distant locations, possibly for airport transfers or special trips.
Geographic visualization helps identify hotspots and patterns in trip locations.

##  Distinct Values

The following fields have distinct values:
- `medallion`: 13,426 unique values
- `hack_license`: 32,224 unique values
- `vendor_id`: 2 unique values
- `rate_code`: 14 unique values
- `store_and_fwd_flag`: 2 unique values
- `pickup_datetime`: 2,303,465 unique values
- `dropoff_datetime`: 2,305,816 unique values
- `passenger_count`: 10 unique values
- `trip_time_in_secs`: 6,594 unique values
- `trip_distance`: 4,368 unique values

### Min/Max Values

Below are the min and max values for key numeric fields:

| **Field Name**         | **Min Value**    | **Max Value**    |
|------------------------|------------------|------------------|
| `passenger_count`      | 0                | 255              |
| `trip_time_in_secs`    | 0                | 10,800           |
| `trip_distance`        | 0                | 100              |

### Average Trip Distance

The **average trip distance** is approximately **3.37 km** based on the filtered data.

### Trip Distance Histogram

A histogram of the trip distances can be found in the project output (refer to images for visualization).

<img src="image2.jpeg" alt="1">

The majority of trips are short distances (0-5 km).
There is an exponential decline, meaning fewer trips occur at longer distances.
There are still some longer trips, but they are much rarer.
This suggests that most taxi trips in this dataset are used for short commutes rather than long-distance travel.

### Average Passengers Per Hour

The average number of passengers per hour of the day was computed and visualized. The chart is available in the project output.

<img src="image3.jpeg" alt="1">

This graph represents the average number of passengers per hour, but only for the full dataset (unlike the first image, which compared full and reduced data).
X-axis (Hour of the Day): 0 to 23, representing each hour.
Y-axis (Average Count): The average number of passengers per trip at that hour.
Observations:
The trend is smoother because it is based on the complete dataset.
A clear dip around 5-6 AM, showing a period of low taxi demand.
A steady increase in passengers throughout the day, peaking in the evening.


### Reduced Dataset

A reduced dataset (1 out of every 1000 rows) was generated and analyzed. A comparison of the analysis results from the reduced dataset versus the full dataset can be found in the project output (refer to the corresponding chart).

<img src="image4.jpeg" alt="1">

- **Blue Line**: Represents the **actual data** (full dataset of all recorded taxi trips).  
- **Red Line**: Represents the **reduced data** (a subset where only 1 out of every 1000 rows was selected).  

### **Detailed Explanation of the Graph**  

1. **X-axis (Hour of Day)**:  
   - Represents the **hour of the day** (0 to 23).  
   - This means that each point on the x-axis corresponds to a specific hour, showing the average number of passengers for trips that started during that hour.  

2. **Y-axis (Average Passengers)**:  
   - Represents the **average number of passengers** per trip for each hour of the day.  
   - The values fluctuate between approximately **1.55 and 1.90** passengers.  

3. **Observations and Trends**:  
   - **Stable Pattern at Midnight to Early Morning (0-4 AM):**  
     - The blue and red lines follow a similar trend, showing a fairly stable average number of passengers.  
   - **Sharp Drop Around 5-6 AM:**  
     - Both lines show a significant decrease in the number of passengers during these early morning hours.  
     - This suggests that very few trips occur at this time, possibly because most people are still at home or sleeping.  
   - **High Variability in the Reduced Dataset (Red Line):**  
     - The red line fluctuates significantly, especially around **4-6 AM**.  
     - This is likely because the reduced dataset (1/1000 rows) does not have enough data points to accurately reflect the actual trend.  
   - **Gradual Increase from Morning to Evening (6 AM - 23 PM):**  
     - After the early morning dip, the number of passengers steadily increases.  
     - This aligns with typical commuting hours, business activities, and evening social outings.  
   - **Red Line Deviations in Some Hours:**  
     - The red line (reduced dataset) sometimes **deviates more** from the blue line.  
     - This is expected because reducing the dataset introduces randomness, leading to **higher variability** in the computed averages.  

### **Key Insights from This Graph**  

- **The actual dataset (blue line) provides a more stable trend**, while the **reduced dataset (red line) shows more fluctuations** due to fewer data points.  
- **There is a noticeable dip in average passenger count between 5-6 AM**, suggesting a low-demand period.  
- **The average number of passengers increases steadily throughout the day**, likely due to increased travel needs during business hours and evening social activities.  
- **Using a reduced dataset can still capture the overall trend, but it introduces more noise and variability.**  

This comparison highlights the **importance of using a sufficiently large dataset for accurate analysis** while also showing that a reduced dataset can still provide useful insights, albeit with some loss of precision.  

## Data Files

This project utilizes the **trip_dat_1.csv** file, which includes the raw data.
