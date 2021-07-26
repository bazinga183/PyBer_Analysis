# PyBer_Analysis

## The Purpose of the Project
The purpose of the new analysis is well defined. (3 pt)
The company V. Isualize has given me the assignment of creating a summary DataFrame for ride-sharing statistics by city-type (Urban, Suburban, Rural). I began this analysis by first getting the necessary files, (city_data.csv)[] and (ride_data.csv)[], merging them so that all the data was in a single data frame, and grouping the rows by their "type" so that new data frames could be created. I created new data columns using these codes:
 
```
total_rides_by_city = pyber_data_df.groupby(["type"]).count()["ride_id"]
total_rides_by_city

driver_count_by_city = city_data_df.groupby(["type"]).sum()["driver_count"]
driver_count_by_city

average_fare_by_city = fare_data_by_city / total_rides_by_city
average_fare_by_city

average_fare_per_driver = fare_data_by_city / driver_count_by_city
average_fare_per_driver
```
Once these were created, I placed them into a new data frame:

```
pyber_summary_df = pd.DataFrame({
    "Total Rides" : total_rides_by_city,
    "Total Drivers" : driver_count_by_city,
    "Total Fares" : fare_data_by_city,
    "Average Fare per Ride" : average_fare_by_city,
    "Average Fare per Driver" : average_fare_per_driver})
pyber_summary_df
```
After, formatting and cleaning up the data, the rest of the project commenced.

## Findings
I took this data frame and grouped it by its fare where the indices were the city type and the date. This allowed me to great a pivot table that had three different columns for urban, suburban, and rural cities. I then created a new data frame using the ``` resample()``` function so that the fare earnings was arranged on a weekly basis.

```
weekly_fare_sums = fare_df.resample("w").sum()
weekly_fare_sums
```

![resample_df](https://user-images.githubusercontent.com/46951897/126935826-71d48313-6e4a-4b6f-a6d5-915691356ec9.JPG)


Finally, I took this data frame and converted it into a line graph where each of the city types were plotted on a weekly basis.

```
weekly_fare_sums.plot(figsize = (15, 5),
                     title = "Total Fare by City Type",
                     grid = True)
plt.ylabel('Fare ($USD)')
plt.xlabel("")

# Import the style from Matplotlib.
from matplotlib import style
# Use the graph style fivethirtyeight.
style.use('fivethirtyeight')
```

![PyBer_fare_summary](https://user-images.githubusercontent.com/46951897/126935994-410519de-bb36-46bd-b61a-a4422d571fdd.png)

## Results
Looking at the visual, it is evident that urban cities outperform in terms of total fares brought in. Suburban and rural cities fall behind heavily, but it is evident that rural cities suffer the most. Even at peak fare earnings, urban cities earn almost 400% more than rural cities and 100% more than suburban cities. 
To put it into perspective, the total fares brought in by urban, suburban, and rural cities are $39,854, $19,356, and $4,328, respectively.

The following data frame was used for the following analysis:

![cities_df](https://user-images.githubusercontent.com/46951897/126935809-395b62b8-4e42-4095-8643-18ba5a7bc5f0.JPG)

A potential reason for this is that the number of rides varies greatly among the three during the first four months of 2019; urban cities had 1625  rides, suburban cities had 625, and rural cities had only 125.
Another notable statistic to note is the total number of drivers within these cities: 
urban cities have 2405 drivers, suburban cities have 490 drivers, and rural cities have only 78 drivers.
Here is where the analysis gets interesting, because despite the immense disparity between the three city types, rural drivers earn more average fare. The average fare per driver in urban, suburban, and rural drivers is $16, $40, and $55, respectively.
In addition, the average fare per ride for urban, suburban, and rural cities is $36, $31, and $25, respectively.
It seems that when there is a scarcity of drivers that the average fare per driver and ride increase. 
There is a description of the differences in ride-sharing data among the different city types. Ride-sharing data include the total rides, total drivers, total fares, average fare per ride and driver, and total fare by city type. (7 pt)

## Summary
In short, urban cities outperform the suburban and rural cities when it comes to totals (rides, drivers, and fares), but suburban and rurals do better when it comes to the averages (fare per driver and ride).

### Recommendations for PyBer
A recommendation that I have for PyBer to address the disparities include:
  - Look into potential projects or incentives that would draw populations into suburban and rural areas to increase the total number of drivers and rides that would be taken in these areas.
  - Find deals or events in urban cities that would increase the total number of rides so that the average fare per driver and rider increase because as it stands, total rides is greater than total drivers and there is an over-saturation of riders in the PyBer market. Either decrease workforce drivers or incentivize riders.
  - Lastly, to increase overall ridership, advertise the green benefits of using a ride-share service and that carpooling with friends and family using PyBer would decrease their carbon footprint. Find ways to make the concept of PyBer appealing to the general crowd.
