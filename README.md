# Case Study 1 How does a bike share navigate speedy success
## 1.Introduction
This project involves a comprehensive analysis of Cyclistic's historical bike trip data to understand the distinct usage patterns of its annual members versus casual riders. The insights gleaned from this analysis are crucial for developing an effective marketing strategy aimed at converting casual riders into annual members, a key objective for the company's future growth and profitability. 

## 2. Scenario
Working as a junior data analyst on Cyclistic's marketing team, the primary goal is to boost annual memberships, which the marketing director sees as vital for the company's future. The team needs to investigate the differences in bike usage patterns between casual riders and annual members. This understanding will be used to create a marketing strategy aimed at converting casual users into annual members. 

## 3. Data analysis
This problem will be addressed using the six steps of the data analysis process :
1. Ask
2. Prepare
3. Process
4. Analyze
5. Share
6. Act

### 3.1 Ask
Creating a marketing program to convert casual riders into members.

The future marketing program will be guided by three key questions:
1. How do annual members and casual riders use Cyclistic bikes differently?
2. Why would casual riders buy Cyclistic annual memberships?
3. How can Cyclistic use digital media to influence casual riders to become members?

### 3.2 Prepare
Data source: Cyclistic's historical trip data, specifically the Divvy 2019 Q1 and Divvy 2020 Q1 datasets.

2019Q1: https://docs.google.com/spreadsheets/d/1uCTsHlZLm4L7-ueaSLwDg0ut3BP_V4mKDo2IMpaXrk4/template/preview?resourcekey=0-dQAUjAu2UUCsLEQQt20PDA#gid=1797029090

2020Q1: https://docs.google.com/spreadsheets/d/179QVLO_yu5BJEKFVZShsKag74ZaUYIF6FevLYzs3hRc/template/preview#gid=640449855

The data source for this analysis consists of two quarterly files: "Divvy 2019 Q1" and "Divvy 2020 Q2". Each file contains details of ride ID, bike type, start time, end time, start station, end station, start location, end location, and member status.

### 3.3 Prepare
Program for data cleaning: R\
<u>The data preparation in R</u>
Import package to do with the data cleaning and load the data
```r
# Load a library
library(tidyverse) 

# Read CSV files
q1_2019 = read_csv("Divvy_Trips_2019_Q1.csv") 
q1_2020 = read_csv("Divvy_Trips_2020_Q1.csv") 
```
The column names in q1_2019.csv are inconsistent with those in q1_2020.csv, necessitating renaming to ensure uniformity.
```r
(q1_2019 = rename(q1_2019
,ride_id = trip_id
,rideable_type = bikeid
,started_at = start_time
,ended_at = end_time
,start_station_name = from_station_name
,start_station_id = from_station_id
,end_station_name = to_station_name
,end_station_id = to_station_id
,member_casual = usertype
))
```
To consolidate the datasets for unified analysis, specific columns like ride_id and rideable_type are converted to character types, ensuring compatibility for stacking the quarterly data into a single comprehensive dataframe. Irrelevant or inconsistent columns, such as personal geographic coordinates, birth year, gender, and tripduration, are then removed to refine the dataset for focused analysis. This meticulous preparation results in a clean, harmonized dataset ready for in-depth exploration.
```r
# Convert ride_id and rideable_type to character so that they can stack correctly
q1_2019 = mutate(q1_2019, ride_id = as.character(ride_id)
,rideable_type = as.character(rideable_type))

# Stack individual quarter's data frames into one big data frame
all_trips = bind_rows(q1_2019, q1_2020)#, q3_2019)#, q4_2019, q1_2020)

# Remove lat, long, birthyear, and gender fields as this data was dropped beginning in 2020
all_trips = all_trips %>%
select(-c(start_lat, start_lng, end_lat, end_lng, birthyear, gender, "tripduration"))
```

```r


```

  
