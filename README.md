# Bellabeat Marketing Analysis: Smart Device Usage Insights

### Introduction

Bellabeat, a high-tech wellness company focused on women's health, has experienced rapid growth since its founding in 2013. With a portfolio of products including the Leaf wellness tracker, Time smartwatch, and Spring smart water bottle, the company aims to empower women with data-driven insights into their health and habits. As a junior data analyst on the Bellabeat marketing analytics team, I have been tasked with analyzing publicly available smart device usage data to uncover trends that can inform the company's marketing strategy and unlock new growth opportunities.


## 1: ASK PHASE

### 1.1: Business Task

This analysis will examine smart device fitness data to understand how consumers are currently using their non-Bellabeat devices. The goal is to translate these behavioral trends into actionable marketing recommendations for the Bellabeat App and broader Bellabeat ecosystem. Specifically, I will address the following guiding questions:

1. **What are some trends in smart device usage?**
2. **How could these trends apply to Bellabeat customers?**
3. **How could these trends help influence Bellabeat marketing strategy?**

The insights derived from this analysis will be presented to the Bellabeat executive team, along with high-level recommendations for marketing strategy (Sršen, 2023).

### 1.2: Key Stakeholders

1. **Urška Sršen:** Bellabeat’s cofounder and Chief Creative Officer
2. **Sando Mur:** Mathematician and Bellabeat’s cofounder; key member of the
     Bellabeat executive team
3. **Bellabeat marketing analytics team:** A team of data analysts responsible for
     collecting, analyzing, and reporting data that helps guide Bellabeat’s
     marketing strategy. 

## 2: PREPARE PHASE

### 2.1: Data Source

The dataset used for this analysis is the **FitBit Fitness Tracker Data**, made available through Mobius on Kaggle (CCO: Public Domain). This dataset contains personal fitness tracker data from over **thirty Fitbit users** who consented to the submission of their personal tracker information. It includes information about daily activity, steps, and heart rate that can be used to explore habits of users.
This dataset provides a comprehensive view of consumer habits and serves as a suitable proxy for understanding how users interact with smart wellness devices in their daily lives.

### 2.2: Data Collection & Storage
The **FitBit Fitness Tracker** dataset was collected from its Kaggle source and appropriately stored and organized in folders and subfolders using conventional file naming methods.  

### 2.3: Data Sorting
The Dataset was overviewed on Excel to determine which would be useful for analysis eg, the daily activity data which contained metrics that can give meaningful insights like total steps taken, calories burnt, active minutes spent etc. Other important data determined to be useful were the sleep day, hourly activity data( steps, calories and intensity) weight log information data and heartrate data. 

### 2.4: Data Credibility Assessment (ROCCC Analysis)

Before proceeding with analysis, it is essential to evaluate the credibility and reliability of the dataset. Using the **ROCCC** framework (Reliable, Original, Comprehensive, Current, and Cited), I assessed the FitBit Fitness Tracker Data to identify potential limitations and ensure the integrity of my findings.

### 2.5: Reliability

The data is sourced from **thirty Fitbit users** who voluntarily consented to share their personal fitness tracker information. While the data appears to be accurately recorded by the Fitbit devices, the sample size is relatively small and may not be representative of the broader population. Additionally, self-reported consent could introduce selection bias, as participants may already be health-conscious individuals.


### 2.6: Currency

The dataset was collected and made available through Kaggle, but the exact collection period is not clearly specified. For a technology-driven analysis, the timeliness of data is critical, as user habits and device capabilities evolve rapidly. This lack of clear temporal context may limit the applicability of findings to current market conditions.


## 3: PROCESS PHASE

### 3.1: Import Libraries


```python
# Import python libraries
 
import pandas as pd
import numpy as np
import warnings
warnings.filterwarnings('ignore')


```

pandas (pd): The most important library for data manipulation. It allows us to work with tabular data (like Excel spreadsheets) using DataFrames.

numpy (np): Provides mathematical functions and array operations. Works behind the scenes with pandas.

warnings: Suppressed warnings to keep our output clean and focused on results.

### 3.2: Import Data Files


```python
# Import data

daily_activity = pd.read_csv("Downloads/bellabeat-case-study/data/raw/dailyActivity_merged.csv")
sleep_day = pd.read_csv("Downloads/bellabeat-case-study/data/raw/sleepDay_merged.csv")
hourly_steps = pd.read_csv("Downloads/bellabeat-case-study/data/raw/hourlySteps_merged.csv")
hourly_calories = pd.read_csv("Downloads/bellabeat-case-study/data/raw/hourlyCalories_merged.csv")
hourly_intensities = pd.read_csv("Downloads/bellabeat-case-study/data/raw/hourlyIntensities_merged.csv")
weight_log_info = pd.read_csv("Downloads/bellabeat-case-study/data/raw/weightLogInfo_merged.csv")
heartrate_seconds = pd.read_csv("Downloads/bellabeat-case-study/data/raw/heartrate_seconds_merged.csv")
```

I represented the data with consistent and descriptive variable names with underscores that allows for code to be easily read and understood. eg, dailyActicity to daily_activity etc.

### 3.3: Explore Each Dataset (Exploratory Data Analysis(EDA))


```python

# Exploring Daily Activity data set.
print("="*50)
print("DAILY ACTIVITY DATA")
print("="*50)
print(f"Shape: {daily_activity.shape}")
print(f"Columns: {daily_activity.columns.tolist()}")
print(f"Data types:\n{daily_activity.dtypes}")
print(f"Missing values:\n{daily_activity.isnull().sum()}")
print(f"Unique users: {daily_activity['Id'].nunique()}")
print("\nFirst 5 rows:")
display(daily_activity.head())
print("\nSummary statistics:")
display(daily_activity.drop('Id',axis=1).describe())

# Exploring Sleep days dataset
print("="*50)
print("SLEEP DAY DATA")
print("="*50)
print(f"Shape: {sleep_day.shape}")
print(f"Columns: {sleep_day.columns.tolist()}")
print(f"Data types:\n{sleep_day.dtypes}")
print(f"Missing values:\n{sleep_day.isnull().sum()}")
print(f"Unique users: {sleep_day['Id'].nunique()}")
print("\nFirst 5 rows:")
display(sleep_day.head())
print("\nSummary statistics:")
display(sleep_day.drop('Id',axis=1).describe())

#Exploring hourly steps dataset
print("="*50)
print("HOURLY STEPS DATA")
print("="*50)
print(f"Shape: {hourly_steps.shape}")
print(f"Columns: {hourly_steps.columns.tolist()}")
print(f"Data types:\n{hourly_steps.dtypes}")
print(f"Missing values:\n{hourly_steps.isnull().sum()}")
print(f"Unique users: {hourly_steps['Id'].nunique()}")
print("\nFirst 5 rows:")
display(hourly_steps.head())
print("\nSummary statistics:")
display(hourly_steps.drop('Id',axis=1).describe())

#Exploring hourly calories dataset
print("="*50)
print("HOURLY CALORIES DATA")
print("="*50)
print(f"Shape: {hourly_calories.shape}")
print(f"Columns: {hourly_calories.columns.tolist()}")
print(f"Data types:\n{hourly_calories.dtypes}")
print(f"Missing values:\n{hourly_calories.isnull().sum()}")
print(f"Unique users: {hourly_calories['Id'].nunique()}")
print("\nFirst 5 rows:")
display(hourly_calories.head())
print("\nSummary statistics:")
display(hourly_calories.drop('Id',axis=1).describe())

#Exploring hourly intensities data
print("="*50)
print("HOURLY INTENSITIES DATA")
print("="*50)
print(f"Shape: {hourly_intensities.shape}")
print(f"Columns: {hourly_intensities.columns.tolist()}")
print(f"Data types:\n{hourly_intensities.dtypes}")
print(f"Missing values:\n{hourly_intensities.isnull().sum()}")
print(f"Unique users: {hourly_intensities['Id'].nunique()}")
print("\nFirst 5 rows:")
display(hourly_intensities.head())
print("\nSummary statistics:")
display(hourly_intensities.drop('Id',axis=1).describe())

#Exploring weight log information data
print("="*50)
print("WEIGHT LOG INFO... DATA")
print("="*50)
print(f"Shape: {weight_log_info.shape}")
print(f"Columns: {weight_log_info.columns.tolist()}")
print(f"Data types:\n{weight_log_info.dtypes}")
print(f"Missing values:\n{weight_log_info.isnull().sum()}")
print(f"Unique users: {weight_log_info['Id'].nunique()}")
print("\nFirst 5 rows:")
display(weight_log_info.head())
print("\nSummary statistics:")
display(weight_log_info.drop('Id', axis=1).describe())

#Exploring heartrate data timed in seconds
print("="*50)
print("HEARTRATE SECONDS DATA")
print("="*50)
print(f"Shape: {heartrate_seconds.shape}")
print(f"Columns: {heartrate_seconds.columns.tolist()}")
print(f"Data types:\n{heartrate_seconds.dtypes}")
print(f"Missing values:\n{heartrate_seconds.isnull().sum()}")
print(f"Unique users: {heartrate_seconds['Id'].nunique()}")
print("\nFirst 5 rows:") 
display(heartrate_seconds.head())
print("\nSummary statistics:")
display(heartrate_seconds.drop('Id',axis = 1).describe())






```

    ==================================================
    DAILY ACTIVITY DATA
    ==================================================
    Shape: (940, 15)
    Columns: ['Id', 'ActivityDate', 'TotalSteps', 'TotalDistance', 'TrackerDistance', 'LoggedActivitiesDistance', 'VeryActiveDistance', 'ModeratelyActiveDistance', 'LightActiveDistance', 'SedentaryActiveDistance', 'VeryActiveMinutes', 'FairlyActiveMinutes', 'LightlyActiveMinutes', 'SedentaryMinutes', 'Calories']
    Data types:
    Id                            int64
    ActivityDate                    str
    TotalSteps                    int64
    TotalDistance               float64
    TrackerDistance             float64
    LoggedActivitiesDistance    float64
    VeryActiveDistance          float64
    ModeratelyActiveDistance    float64
    LightActiveDistance         float64
    SedentaryActiveDistance     float64
    VeryActiveMinutes             int64
    FairlyActiveMinutes           int64
    LightlyActiveMinutes          int64
    SedentaryMinutes              int64
    Calories                      int64
    dtype: object
    Missing values:
    Id                          0
    ActivityDate                0
    TotalSteps                  0
    TotalDistance               0
    TrackerDistance             0
    LoggedActivitiesDistance    0
    VeryActiveDistance          0
    ModeratelyActiveDistance    0
    LightActiveDistance         0
    SedentaryActiveDistance     0
    VeryActiveMinutes           0
    FairlyActiveMinutes         0
    LightlyActiveMinutes        0
    SedentaryMinutes            0
    Calories                    0
    dtype: int64
    Unique users: 33
    
    First 5 rows:
    


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Id</th>
      <th>ActivityDate</th>
      <th>TotalSteps</th>
      <th>TotalDistance</th>
      <th>TrackerDistance</th>
      <th>LoggedActivitiesDistance</th>
      <th>VeryActiveDistance</th>
      <th>ModeratelyActiveDistance</th>
      <th>LightActiveDistance</th>
      <th>SedentaryActiveDistance</th>
      <th>VeryActiveMinutes</th>
      <th>FairlyActiveMinutes</th>
      <th>LightlyActiveMinutes</th>
      <th>SedentaryMinutes</th>
      <th>Calories</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1503960366</td>
      <td>4/12/2016</td>
      <td>13162</td>
      <td>8.50</td>
      <td>8.50</td>
      <td>0.0</td>
      <td>1.88</td>
      <td>0.55</td>
      <td>6.06</td>
      <td>0.0</td>
      <td>25</td>
      <td>13</td>
      <td>328</td>
      <td>728</td>
      <td>1985</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1503960366</td>
      <td>4/13/2016</td>
      <td>10735</td>
      <td>6.97</td>
      <td>6.97</td>
      <td>0.0</td>
      <td>1.57</td>
      <td>0.69</td>
      <td>4.71</td>
      <td>0.0</td>
      <td>21</td>
      <td>19</td>
      <td>217</td>
      <td>776</td>
      <td>1797</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1503960366</td>
      <td>4/14/2016</td>
      <td>10460</td>
      <td>6.74</td>
      <td>6.74</td>
      <td>0.0</td>
      <td>2.44</td>
      <td>0.40</td>
      <td>3.91</td>
      <td>0.0</td>
      <td>30</td>
      <td>11</td>
      <td>181</td>
      <td>1218</td>
      <td>1776</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1503960366</td>
      <td>4/15/2016</td>
      <td>9762</td>
      <td>6.28</td>
      <td>6.28</td>
      <td>0.0</td>
      <td>2.14</td>
      <td>1.26</td>
      <td>2.83</td>
      <td>0.0</td>
      <td>29</td>
      <td>34</td>
      <td>209</td>
      <td>726</td>
      <td>1745</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1503960366</td>
      <td>4/16/2016</td>
      <td>12669</td>
      <td>8.16</td>
      <td>8.16</td>
      <td>0.0</td>
      <td>2.71</td>
      <td>0.41</td>
      <td>5.04</td>
      <td>0.0</td>
      <td>36</td>
      <td>10</td>
      <td>221</td>
      <td>773</td>
      <td>1863</td>
    </tr>
  </tbody>
</table>
</div>


    
    Summary statistics:
    


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>TotalSteps</th>
      <th>TotalDistance</th>
      <th>TrackerDistance</th>
      <th>LoggedActivitiesDistance</th>
      <th>VeryActiveDistance</th>
      <th>ModeratelyActiveDistance</th>
      <th>LightActiveDistance</th>
      <th>SedentaryActiveDistance</th>
      <th>VeryActiveMinutes</th>
      <th>FairlyActiveMinutes</th>
      <th>LightlyActiveMinutes</th>
      <th>SedentaryMinutes</th>
      <th>Calories</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>940.000000</td>
      <td>940.000000</td>
      <td>940.000000</td>
      <td>940.000000</td>
      <td>940.000000</td>
      <td>940.000000</td>
      <td>940.000000</td>
      <td>940.000000</td>
      <td>940.000000</td>
      <td>940.000000</td>
      <td>940.000000</td>
      <td>940.000000</td>
      <td>940.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>7637.910638</td>
      <td>5.489702</td>
      <td>5.475351</td>
      <td>0.108171</td>
      <td>1.502681</td>
      <td>0.567543</td>
      <td>3.340819</td>
      <td>0.001606</td>
      <td>21.164894</td>
      <td>13.564894</td>
      <td>192.812766</td>
      <td>991.210638</td>
      <td>2303.609574</td>
    </tr>
    <tr>
      <th>std</th>
      <td>5087.150742</td>
      <td>3.924606</td>
      <td>3.907276</td>
      <td>0.619897</td>
      <td>2.658941</td>
      <td>0.883580</td>
      <td>2.040655</td>
      <td>0.007346</td>
      <td>32.844803</td>
      <td>19.987404</td>
      <td>109.174700</td>
      <td>301.267437</td>
      <td>718.166862</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>3789.750000</td>
      <td>2.620000</td>
      <td>2.620000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.945000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>127.000000</td>
      <td>729.750000</td>
      <td>1828.500000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>7405.500000</td>
      <td>5.245000</td>
      <td>5.245000</td>
      <td>0.000000</td>
      <td>0.210000</td>
      <td>0.240000</td>
      <td>3.365000</td>
      <td>0.000000</td>
      <td>4.000000</td>
      <td>6.000000</td>
      <td>199.000000</td>
      <td>1057.500000</td>
      <td>2134.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>10727.000000</td>
      <td>7.712500</td>
      <td>7.710000</td>
      <td>0.000000</td>
      <td>2.052500</td>
      <td>0.800000</td>
      <td>4.782500</td>
      <td>0.000000</td>
      <td>32.000000</td>
      <td>19.000000</td>
      <td>264.000000</td>
      <td>1229.500000</td>
      <td>2793.250000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>36019.000000</td>
      <td>28.030001</td>
      <td>28.030001</td>
      <td>4.942142</td>
      <td>21.920000</td>
      <td>6.480000</td>
      <td>10.710000</td>
      <td>0.110000</td>
      <td>210.000000</td>
      <td>143.000000</td>
      <td>518.000000</td>
      <td>1440.000000</td>
      <td>4900.000000</td>
    </tr>
  </tbody>
</table>
</div>


    ==================================================
    SLEEP DAY DATA
    ==================================================
    Shape: (413, 5)
    Columns: ['Id', 'SleepDay', 'TotalSleepRecords', 'TotalMinutesAsleep', 'TotalTimeInBed']
    Data types:
    Id                    int64
    SleepDay                str
    TotalSleepRecords     int64
    TotalMinutesAsleep    int64
    TotalTimeInBed        int64
    dtype: object
    Missing values:
    Id                    0
    SleepDay              0
    TotalSleepRecords     0
    TotalMinutesAsleep    0
    TotalTimeInBed        0
    dtype: int64
    Unique users: 24
    
    First 5 rows:
    


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Id</th>
      <th>SleepDay</th>
      <th>TotalSleepRecords</th>
      <th>TotalMinutesAsleep</th>
      <th>TotalTimeInBed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1503960366</td>
      <td>4/12/2016 12:00:00 AM</td>
      <td>1</td>
      <td>327</td>
      <td>346</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1503960366</td>
      <td>4/13/2016 12:00:00 AM</td>
      <td>2</td>
      <td>384</td>
      <td>407</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1503960366</td>
      <td>4/15/2016 12:00:00 AM</td>
      <td>1</td>
      <td>412</td>
      <td>442</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1503960366</td>
      <td>4/16/2016 12:00:00 AM</td>
      <td>2</td>
      <td>340</td>
      <td>367</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1503960366</td>
      <td>4/17/2016 12:00:00 AM</td>
      <td>1</td>
      <td>700</td>
      <td>712</td>
    </tr>
  </tbody>
</table>
</div>


    
    Summary statistics:
    


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>TotalSleepRecords</th>
      <th>TotalMinutesAsleep</th>
      <th>TotalTimeInBed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>413.000000</td>
      <td>413.000000</td>
      <td>413.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>1.118644</td>
      <td>419.467312</td>
      <td>458.639225</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.345521</td>
      <td>118.344679</td>
      <td>127.101607</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.000000</td>
      <td>58.000000</td>
      <td>61.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>1.000000</td>
      <td>361.000000</td>
      <td>403.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>1.000000</td>
      <td>433.000000</td>
      <td>463.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>1.000000</td>
      <td>490.000000</td>
      <td>526.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>3.000000</td>
      <td>796.000000</td>
      <td>961.000000</td>
    </tr>
  </tbody>
</table>
</div>


    ==================================================
    HOURLY STEPS DATA
    ==================================================
    Shape: (22099, 3)
    Columns: ['Id', 'ActivityHour', 'StepTotal']
    Data types:
    Id              int64
    ActivityHour      str
    StepTotal       int64
    dtype: object
    Missing values:
    Id              0
    ActivityHour    0
    StepTotal       0
    dtype: int64
    Unique users: 33
    
    First 5 rows:
    


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Id</th>
      <th>ActivityHour</th>
      <th>StepTotal</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1503960366</td>
      <td>4/12/2016 12:00:00 AM</td>
      <td>373</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1503960366</td>
      <td>4/12/2016 1:00:00 AM</td>
      <td>160</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1503960366</td>
      <td>4/12/2016 2:00:00 AM</td>
      <td>151</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1503960366</td>
      <td>4/12/2016 3:00:00 AM</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1503960366</td>
      <td>4/12/2016 4:00:00 AM</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>


    
    Summary statistics:
    


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>StepTotal</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>22099.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>320.166342</td>
    </tr>
    <tr>
      <th>std</th>
      <td>690.384228</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>40.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>357.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>10554.000000</td>
    </tr>
  </tbody>
</table>
</div>


    ==================================================
    HOURLY CALORIES DATA
    ==================================================
    Shape: (22099, 3)
    Columns: ['Id', 'ActivityHour', 'Calories']
    Data types:
    Id              int64
    ActivityHour      str
    Calories        int64
    dtype: object
    Missing values:
    Id              0
    ActivityHour    0
    Calories        0
    dtype: int64
    Unique users: 33
    
    First 5 rows:
    


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Id</th>
      <th>ActivityHour</th>
      <th>Calories</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1503960366</td>
      <td>4/12/2016 12:00:00 AM</td>
      <td>81</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1503960366</td>
      <td>4/12/2016 1:00:00 AM</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1503960366</td>
      <td>4/12/2016 2:00:00 AM</td>
      <td>59</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1503960366</td>
      <td>4/12/2016 3:00:00 AM</td>
      <td>47</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1503960366</td>
      <td>4/12/2016 4:00:00 AM</td>
      <td>48</td>
    </tr>
  </tbody>
</table>
</div>


    
    Summary statistics:
    


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Calories</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>22099.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>97.386760</td>
    </tr>
    <tr>
      <th>std</th>
      <td>60.702622</td>
    </tr>
    <tr>
      <th>min</th>
      <td>42.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>63.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>83.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>108.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>948.000000</td>
    </tr>
  </tbody>
</table>
</div>


    ==================================================
    HOURLY INTENSITIES DATA
    ==================================================
    Shape: (22099, 4)
    Columns: ['Id', 'ActivityHour', 'TotalIntensity', 'AverageIntensity']
    Data types:
    Id                    int64
    ActivityHour            str
    TotalIntensity        int64
    AverageIntensity    float64
    dtype: object
    Missing values:
    Id                  0
    ActivityHour        0
    TotalIntensity      0
    AverageIntensity    0
    dtype: int64
    Unique users: 33
    
    First 5 rows:
    


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Id</th>
      <th>ActivityHour</th>
      <th>TotalIntensity</th>
      <th>AverageIntensity</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1503960366</td>
      <td>4/12/2016 12:00:00 AM</td>
      <td>20</td>
      <td>0.333333</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1503960366</td>
      <td>4/12/2016 1:00:00 AM</td>
      <td>8</td>
      <td>0.133333</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1503960366</td>
      <td>4/12/2016 2:00:00 AM</td>
      <td>7</td>
      <td>0.116667</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1503960366</td>
      <td>4/12/2016 3:00:00 AM</td>
      <td>0</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1503960366</td>
      <td>4/12/2016 4:00:00 AM</td>
      <td>0</td>
      <td>0.000000</td>
    </tr>
  </tbody>
</table>
</div>


    
    Summary statistics:
    


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>TotalIntensity</th>
      <th>AverageIntensity</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>22099.000000</td>
      <td>22099.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>12.035341</td>
      <td>0.200589</td>
    </tr>
    <tr>
      <th>std</th>
      <td>21.133110</td>
      <td>0.352219</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>3.000000</td>
      <td>0.050000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>16.000000</td>
      <td>0.266667</td>
    </tr>
    <tr>
      <th>max</th>
      <td>180.000000</td>
      <td>3.000000</td>
    </tr>
  </tbody>
</table>
</div>


    ==================================================
    WEIGHT LOG INFO... DATA
    ==================================================
    Shape: (67, 8)
    Columns: ['Id', 'Date', 'WeightKg', 'WeightPounds', 'Fat', 'BMI', 'IsManualReport', 'LogId']
    Data types:
    Id                  int64
    Date                  str
    WeightKg          float64
    WeightPounds      float64
    Fat               float64
    BMI               float64
    IsManualReport       bool
    LogId               int64
    dtype: object
    Missing values:
    Id                 0
    Date               0
    WeightKg           0
    WeightPounds       0
    Fat               65
    BMI                0
    IsManualReport     0
    LogId              0
    dtype: int64
    Unique users: 8
    
    First 5 rows:
    


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Id</th>
      <th>Date</th>
      <th>WeightKg</th>
      <th>WeightPounds</th>
      <th>Fat</th>
      <th>BMI</th>
      <th>IsManualReport</th>
      <th>LogId</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1503960366</td>
      <td>5/2/2016 11:59:59 PM</td>
      <td>52.599998</td>
      <td>115.963147</td>
      <td>22.0</td>
      <td>22.650000</td>
      <td>True</td>
      <td>1462233599000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1503960366</td>
      <td>5/3/2016 11:59:59 PM</td>
      <td>52.599998</td>
      <td>115.963147</td>
      <td>NaN</td>
      <td>22.650000</td>
      <td>True</td>
      <td>1462319999000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1927972279</td>
      <td>4/13/2016 1:08:52 AM</td>
      <td>133.500000</td>
      <td>294.317120</td>
      <td>NaN</td>
      <td>47.540001</td>
      <td>False</td>
      <td>1460509732000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2873212765</td>
      <td>4/21/2016 11:59:59 PM</td>
      <td>56.700001</td>
      <td>125.002104</td>
      <td>NaN</td>
      <td>21.450001</td>
      <td>True</td>
      <td>1461283199000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2873212765</td>
      <td>5/12/2016 11:59:59 PM</td>
      <td>57.299999</td>
      <td>126.324875</td>
      <td>NaN</td>
      <td>21.690001</td>
      <td>True</td>
      <td>1463097599000</td>
    </tr>
  </tbody>
</table>
</div>


    
    Summary statistics:
    


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>WeightKg</th>
      <th>WeightPounds</th>
      <th>Fat</th>
      <th>BMI</th>
      <th>LogId</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>67.000000</td>
      <td>67.000000</td>
      <td>2.00000</td>
      <td>67.000000</td>
      <td>6.700000e+01</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>72.035821</td>
      <td>158.811801</td>
      <td>23.50000</td>
      <td>25.185224</td>
      <td>1.461772e+12</td>
    </tr>
    <tr>
      <th>std</th>
      <td>13.923206</td>
      <td>30.695415</td>
      <td>2.12132</td>
      <td>3.066963</td>
      <td>7.829948e+08</td>
    </tr>
    <tr>
      <th>min</th>
      <td>52.599998</td>
      <td>115.963147</td>
      <td>22.00000</td>
      <td>21.450001</td>
      <td>1.460444e+12</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>61.400002</td>
      <td>135.363832</td>
      <td>22.75000</td>
      <td>23.959999</td>
      <td>1.461079e+12</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>62.500000</td>
      <td>137.788914</td>
      <td>23.50000</td>
      <td>24.389999</td>
      <td>1.461802e+12</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>85.049999</td>
      <td>187.503152</td>
      <td>24.25000</td>
      <td>25.559999</td>
      <td>1.462375e+12</td>
    </tr>
    <tr>
      <th>max</th>
      <td>133.500000</td>
      <td>294.317120</td>
      <td>25.00000</td>
      <td>47.540001</td>
      <td>1.463098e+12</td>
    </tr>
  </tbody>
</table>
</div>


    ==================================================
    HEARTRATE SECONDS DATA
    ==================================================
    Shape: (2483658, 3)
    Columns: ['Id', 'Time', 'Value']
    Data types:
    Id       int64
    Time       str
    Value    int64
    dtype: object
    Missing values:
    Id       0
    Time     0
    Value    0
    dtype: int64
    Unique users: 14
    
    First 5 rows:
    


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Id</th>
      <th>Time</th>
      <th>Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2022484408</td>
      <td>4/12/2016 7:21:00 AM</td>
      <td>97</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2022484408</td>
      <td>4/12/2016 7:21:05 AM</td>
      <td>102</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2022484408</td>
      <td>4/12/2016 7:21:10 AM</td>
      <td>105</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2022484408</td>
      <td>4/12/2016 7:21:20 AM</td>
      <td>103</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2022484408</td>
      <td>4/12/2016 7:21:25 AM</td>
      <td>101</td>
    </tr>
  </tbody>
</table>
</div>


    
    Summary statistics:
    


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>2.483658e+06</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>7.732842e+01</td>
    </tr>
    <tr>
      <th>std</th>
      <td>1.940450e+01</td>
    </tr>
    <tr>
      <th>min</th>
      <td>3.600000e+01</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>6.300000e+01</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>7.300000e+01</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>8.800000e+01</td>
    </tr>
    <tr>
      <th>max</th>
      <td>2.030000e+02</td>
    </tr>
  </tbody>
</table>
</div>


#### EDA SUMMARY

* I needed to understand what data i have, did this by checking the shape of datasets, colunms involved and their data types.

* I checked for missing values, all had no missing values except waight log info data where the colunm for fat had 64 missing values.

* Hourly steps and calories has similar structure of 22099 rows and 3 colunms so they can be merged into one for further analysis.

* Average total steps per day is around 7,600 which is fairly okay for people who excersice but could be improved. 

* Average sedentary minutes is almost 1000 minutes(over 16 hours) this is quite alot and has to reduce. 

* I verified that data types are correct, noticed that IDs were numbers so i will have to convert them to text in cleaning phase.

* I checked to see how many users are in each dataset - important because some users may not have all types of data.
There is 33 users in the daily activity, hourly calories, hourly intensities and hourly steps data sets, 24 in the sleep, 14 in heartrate and only 8 in the weight data set. None of these numbers is enough to make any conclusions but i will proceed for sake of this project and drop weight log data cause 8 users is way too small for any form of analysis.

### 3.4: Check For Duplicates and Data Quality (Data Cleaning)


```python
# Check for duplicates in each dataset

print("Duplicate rows before cleaning:")
print(f"Daily Activity: {daily_activity.duplicated().sum()}")
print(f"Sleep Day: {sleep_day.duplicated().sum()}")
print(f"Hourly Steps: {hourly_steps.duplicated().sum()}")
print(f"Hourly Calories: {hourly_calories.duplicated().sum()}")
print(f"Hourly Intensities: {hourly_intensities.duplicated().sum()}")
print(f"Weight Log: {weight_log_info.duplicated().sum()}")
print(f"Heartrate Seconds: {heartrate_seconds.duplicated().sum()}")

# Remove duplicates

daily_activity = daily_activity.drop_duplicates()
sleep_day = sleep_day.drop_duplicates()
hourly_steps = hourly_steps.drop_duplicates()
hourly_calories = hourly_calories.drop_duplicates()
hourly_intensities = hourly_intensities.drop_duplicates()
weight_log_info = weight_log_info.drop_duplicates()
heartrate_seconds = heartrate_seconds.drop_duplicates()

# Confirm duplicates have been removed

print("\nDuplicate rows after cleaning:")
print(f"Daily Activity: {daily_activity.duplicated().sum()}")
print(f"Sleep Day: {sleep_day.duplicated().sum()}")
print(f"Hourly Steps: {hourly_steps.duplicated().sum()}")
print(f"Hourly Calories: {hourly_calories.duplicated().sum()}")
print(f"Hourly Intensities: {hourly_intensities.duplicated().sum()}")
print(f"Weight Log: {weight_log_info.duplicated().sum()}")
print(f"Heartrate Seconds: {heartrate_seconds.duplicated().sum()}")

```

    Duplicate rows before cleaning:
    Daily Activity: 0
    Sleep Day: 3
    Hourly Steps: 0
    Hourly Calories: 0
    Hourly Intensities: 0
    Weight Log: 0
    Heartrate Seconds: 0
    
    Duplicate rows after cleaning:
    Daily Activity: 0
    Sleep Day: 0
    Hourly Steps: 0
    Hourly Calories: 0
    Hourly Intensities: 0
    Weight Log: 0
    Heartrate Seconds: 0
    

##### Explanation
* All datasets were free of duplicates except sleep day which had 3 duplicates because same day was recorded multiple times.
* Duplicates would skew analysis (eg, average a value twice) so removed them and confirmed there are no more duplicates.

### 3.5: Convert Data Types


```python
# Convert ID to string for all datasets
datasets = [daily_activity, sleep_day, hourly_steps, hourly_calories, 
            hourly_intensities, weight_log_info, heartrate_seconds]
for df in datasets:
    df['Id'] = df['Id'].astype('object')

# Confirm ID column conversion for all datasets
print("=== ID COLUMN DATA TYPE VERIFICATION FOR EACH DATASET ===\n")
for df in datasets:
    # Get the dataframe name (optional - requires naming)
    print(f"ID dtype: {df['Id'].dtype}")

```

    === ID COLUMN DATA TYPE VERIFICATION FOR EACH DATASET ===
    
    ID dtype: object
    ID dtype: object
    ID dtype: object
    ID dtype: object
    ID dtype: object
    ID dtype: object
    ID dtype: object
    

##### Explanation
* User Ids are identifiers and not numbers to perform math on.
* I had to convert them to the general python object datatype, preventing python from treating them as numbers and performing calculations on them.
* Checked that Ids have been converted on all colunms without having tp print colunm names.

### 3.6: Convert Date/Time colunms


```python
# Daily Activity - convert ActivityDate
daily_activity['ActivityDate'] = pd.to_datetime(daily_activity['ActivityDate'], format='%m/%d/%Y')

# Sleep Day - convert SleepDay
sleep_day['SleepDay'] = pd.to_datetime(sleep_day['SleepDay'], format='%m/%d/%Y %I:%M:%S %p')

# Hourly data - convert ActivityHour
hourly_steps['ActivityHour'] = pd.to_datetime(hourly_steps['ActivityHour'], format='%m/%d/%Y %I:%M:%S %p')
hourly_calories['ActivityHour'] = pd.to_datetime(hourly_calories['ActivityHour'], format='%m/%d/%Y %I:%M:%S %p')
hourly_intensities['ActivityHour'] = pd.to_datetime(hourly_intensities['ActivityHour'], format='%m/%d/%Y %I:%M:%S %p')

# Weight Log Info - convert Date
weight_log_info['Date'] = pd.to_datetime(weight_log_info['Date'], format='%m/%d/%Y %I:%M:%S %p')

# Heart Rate - convert Time
heartrate_seconds['Time'] = pd.to_datetime(heartrate_seconds['Time'], format='%m/%d/%Y %I:%M:%S %p')
```


```python
 # Check date/time data types for all datasets
print("=== Date/Time Data Types After Conversion ===")
print(f"Daily Activity: {daily_activity['ActivityDate'].dtype}")
print(f"Sleep Day: {sleep_day['SleepDay'].dtype}")
print(f"Hourly Steps: {hourly_steps['ActivityHour'].dtype}")
print(f"Hourly Calories: {hourly_calories['ActivityHour'].dtype}")
print(f"Hourly Intensities: {hourly_intensities['ActivityHour'].dtype}")
print(f"Weight Log: {weight_log_info['Date'].dtype}")
print(f"Heartrate: {heartrate_seconds['Time'].dtype}")
```

    === Date/Time Data Types After Conversion ===
    Daily Activity: datetime64[us]
    Sleep Day: datetime64[us]
    Hourly Steps: datetime64[us]
    Hourly Calories: datetime64[us]
    Hourly Intensities: datetime64[us]
    Weight Log: datetime64[us]
    Heartrate: datetime64[us]
    

##### Explanation

All datasets were successfully converted to datetime64 format 
(microsecond precision). This allows for:

✅ Chronological sorting
✅ Day-of-week extraction
✅ Time-based calculations
✅ Date filtering and grouping

### 3.7: Create New Features(Derived Colunms)


```python
# Sleep Day - calculate sleep efficiency
sleep_day['SleepEfficiency'] = (sleep_day['TotalMinutesAsleep'] / sleep_day['TotalTimeInBed']) * 100

# Daily Activity - calculate total active minutes
daily_activity['TotalActiveMinutes'] = (daily_activity['VeryActiveMinutes'] + 
                                        daily_activity['FairlyActiveMinutes'] + 
                                        daily_activity['LightlyActiveMinutes'])
# Daily Activity - calculate sedentary percentage 
daily_activity['SedentaryPercentage'] = (daily_activity['SedentaryMinutes'] / 
                                         (daily_activity['TotalActiveMinutes'] + daily_activity['SedentaryMinutes'])) * 100


# Confirm new columns by extracting them from their datasets
sleep_new_col = sleep_day[['SleepEfficiency']].head()
activity_new_cols = daily_activity[['TotalActiveMinutes', 'SedentaryPercentage']].head()

# Combine them side-by-side
combined = pd.concat([sleep_new_col, activity_new_cols], axis=1)

print("✅ New columns verified (first 5 rows):")
print(combined)
```

    ✅ New columns verified (first 5 rows):
       SleepEfficiency  TotalActiveMinutes  SedentaryPercentage
    0        94.508671                 366            66.544790
    1        94.348894                 257            75.121007
    2        93.212670                 222            84.583333
    3        92.643052                 272            72.745491
    4        98.314607                 267            74.326923
    

##### Eplanation of new columns
* Sleep Efficiency: Shows what percentage of time in bed is actually spent sleeping.

* Total Active Minutes: Sum of all active minutes regardless of intensity.

* Sedentary Percentage: What percentage of the day is spent sitting/being inactive.
  Helps identify users who are too sedentary

##### Why i did this:

* The raw data doesn't include these metrics, but they're more meaningful for analysis

* Sleep efficiency is a better measure of sleep quality than just total time asleep

* Understanding activity vs. sedentary time helps identify health risks

### 3.8: Aggregate Heart Rate Data


```python
# Extract date from timestamp
heartrate_seconds['Date'] = heartrate_seconds['Time'].dt.date

# Group by user and date to get daily statistics
heart_rate_daily = heartrate_seconds.groupby(['Id', 'Date']).agg(
    avg_heart_rate=('Value', 'mean'),
    min_heart_rate=('Value', 'min'),
    max_heart_rate=('Value', 'max'),
).reset_index()

# Convert Date back to datetime
heart_rate_daily['Date'] = pd.to_datetime(heart_rate_daily['Date'])

# Preview aggregared heart rate table
heart_rate_daily.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Id</th>
      <th>Date</th>
      <th>avg_heart_rate</th>
      <th>min_heart_rate</th>
      <th>max_heart_rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2022484408</td>
      <td>2016-04-12</td>
      <td>75.804177</td>
      <td>52</td>
      <td>134</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2022484408</td>
      <td>2016-04-13</td>
      <td>80.337584</td>
      <td>51</td>
      <td>156</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2022484408</td>
      <td>2016-04-14</td>
      <td>72.628597</td>
      <td>50</td>
      <td>127</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2022484408</td>
      <td>2016-04-15</td>
      <td>80.437382</td>
      <td>53</td>
      <td>189</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2022484408</td>
      <td>2016-04-16</td>
      <td>75.960547</td>
      <td>49</td>
      <td>136</td>
    </tr>
  </tbody>
</table>
</div>



#### Why i did this:

* The heart rate file is enormous (millions of rows at the second level)

* I couldn't work with this much data efficiently

* Aggregating to daily level makes the data manageable while keeping the key information

* Average daily heart rate is more meaningful for my analysis than individual second-by-second readings

### 3.9: Merge Datasets


```python
# Rename date columns to match
sleep_day = sleep_day.rename(columns={'SleepDay': 'Date'})
daily_activity = daily_activity.rename(columns={'ActivityDate': 'Date'})

# Now merge sleep and daily activity
merged_data = pd.merge(sleep_day, daily_activity,
    on=['Id', 'Date'],
    how='inner')

# Merge with aggregated daily heart rate data
merged_data = pd.merge(merged_data, heart_rate_daily, 
                       on=['Id', 'Date'], 
                       how='inner')

# Preview final merged table
merged_data.head()


```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Id</th>
      <th>Date</th>
      <th>TotalSleepRecords</th>
      <th>TotalMinutesAsleep</th>
      <th>TotalTimeInBed</th>
      <th>SleepEfficiency</th>
      <th>TotalSteps</th>
      <th>TotalDistance</th>
      <th>TrackerDistance</th>
      <th>LoggedActivitiesDistance</th>
      <th>...</th>
      <th>VeryActiveMinutes</th>
      <th>FairlyActiveMinutes</th>
      <th>LightlyActiveMinutes</th>
      <th>SedentaryMinutes</th>
      <th>Calories</th>
      <th>TotalActiveMinutes</th>
      <th>SedentaryPercentage</th>
      <th>avg_heart_rate</th>
      <th>min_heart_rate</th>
      <th>max_heart_rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2026352035</td>
      <td>2016-04-17</td>
      <td>1</td>
      <td>437</td>
      <td>498</td>
      <td>87.751004</td>
      <td>838</td>
      <td>0.52</td>
      <td>0.52</td>
      <td>0.0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>60</td>
      <td>1053</td>
      <td>1214</td>
      <td>60</td>
      <td>94.609164</td>
      <td>68.656250</td>
      <td>63</td>
      <td>80</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2026352035</td>
      <td>2016-04-25</td>
      <td>1</td>
      <td>506</td>
      <td>531</td>
      <td>95.291902</td>
      <td>6017</td>
      <td>3.73</td>
      <td>3.73</td>
      <td>0.0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>260</td>
      <td>821</td>
      <td>1576</td>
      <td>260</td>
      <td>75.948196</td>
      <td>99.505814</td>
      <td>70</td>
      <td>125</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2026352035</td>
      <td>2016-05-02</td>
      <td>1</td>
      <td>511</td>
      <td>543</td>
      <td>94.106814</td>
      <td>7018</td>
      <td>4.35</td>
      <td>4.35</td>
      <td>0.0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>355</td>
      <td>716</td>
      <td>1690</td>
      <td>355</td>
      <td>66.853408</td>
      <td>84.134571</td>
      <td>70</td>
      <td>122</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2026352035</td>
      <td>2016-05-09</td>
      <td>1</td>
      <td>531</td>
      <td>556</td>
      <td>95.503597</td>
      <td>10685</td>
      <td>6.62</td>
      <td>6.62</td>
      <td>0.0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>401</td>
      <td>543</td>
      <td>1869</td>
      <td>401</td>
      <td>57.521186</td>
      <td>98.233901</td>
      <td>70</td>
      <td>123</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2347167796</td>
      <td>2016-04-13</td>
      <td>1</td>
      <td>467</td>
      <td>531</td>
      <td>87.947269</td>
      <td>10352</td>
      <td>7.01</td>
      <td>7.01</td>
      <td>0.0</td>
      <td>...</td>
      <td>19</td>
      <td>32</td>
      <td>195</td>
      <td>676</td>
      <td>2038</td>
      <td>246</td>
      <td>73.318872</td>
      <td>73.812905</td>
      <td>55</td>
      <td>158</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 24 columns</p>
</div>




```python
# Drop AverageIntensity column (we don't need it)
hourly_intensities = hourly_intensities.drop('AverageIntensity', axis=1, errors='ignore')

# Merge steps and calories first
hourly_steps_calories = pd.merge(hourly_steps, hourly_calories, 
                                 on=['Id', 'ActivityHour'], 
                                 how='inner')

# Merge with intensities (now has same 3 columns structure)
hourly_activity = pd.merge(hourly_steps_calories, hourly_intensities,
                           on=['Id', 'ActivityHour'],
                           how='inner')
# Extract hour from ActivityHour
hourly_activity['Hour'] = hourly_activity['ActivityHour'].dt.hour

# Preview hourly activity table
hourly_activity.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Id</th>
      <th>ActivityHour</th>
      <th>StepTotal</th>
      <th>Calories</th>
      <th>TotalIntensity</th>
      <th>Hour</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1503960366</td>
      <td>2016-04-12 00:00:00</td>
      <td>373</td>
      <td>81</td>
      <td>20</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1503960366</td>
      <td>2016-04-12 01:00:00</td>
      <td>160</td>
      <td>61</td>
      <td>8</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1503960366</td>
      <td>2016-04-12 02:00:00</td>
      <td>151</td>
      <td>59</td>
      <td>7</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1503960366</td>
      <td>2016-04-12 03:00:00</td>
      <td>0</td>
      <td>47</td>
      <td>0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1503960366</td>
      <td>2016-04-12 04:00:00</td>
      <td>0</td>
      <td>48</td>
      <td>0</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>



#### Explanation

I wanted to merge sleep, daily activity and daily heart rate data together but sleep and daily activity data had different column names for their dates even though dates are the same so i had so rename their columns to "Date" so they can match and be merged easily. I also merged hourly steps, calories and intensity data by first removing average intensity column from hourly intensity table cause it`s not useful for my analysis and this made hourly intensity data have same shape with hourly steps and calories data which inturn made merging of all three easier and void of null values. I also extracted "Hour" from the ActivityHoul column because that's the exact metric i need any analysis with hourly activity data.

#### Why i did this:

* I want to analyze the relationships between sleep and activity

* I also want to do hourly pattern analysis

* I can answer questions surrounding hourly activities (steps taken, calories burnt, intensity levels)

* With merged dleep and daily activity data, i can answer questions like "Does more activity lead to better sleep?"


### 3.10: Explore User Engagement


```python
# Count records per user for each dataset
user_activity_count = daily_activity.groupby('Id')['Date'].count().sort_values(ascending=False)
user_sleep_count = sleep_day.groupby('Id')['Date'].count().sort_values(ascending=False)

print("\nUser Engagement Summary:")
print(f"Active users (with daily activity): {len(user_activity_count)}")
print(f"Users with sleep data: {len(user_sleep_count)}")
print(f"Users with heart rate data: {heart_rate_daily['Id'].nunique()}")
print(f"Users with weight data: {weight_log_info['Id'].nunique()}")
```

    
    User Engagement Summary:
    Active users (with daily activity): 33
    Users with sleep data: 24
    Users with heart rate data: 14
    Users with weight data: 8
    

#### Why I did this:

* Not all users have all types of data

* Understanding engagement helps us know who we can analyze

* Users with more data are more valuable for trend analysis



## 4: ANALYZE PHASE

#### Now i have two datasets left after processing which are :

* merged_data : A combination of daily activity, sleep days and aggregated heart rate datasets
* hourly_activity : A combination of hourly steps, calories and intensities data after dropping column for averahe intensities in hourly intensities table.

### 4.1: Data Structure Verification


```python
# ==========================================
# 1. VERIFY YOUR DATA STRUCTURE
# ==========================================

print("="*60)
print("BELLABEAT CASE STUDY - ANALYSIS PHASE")
print("="*60)

print(f"\n📊 Daily Data: {merged_data.shape[0]} rows, {merged_data.shape[1]} columns, {merged_data['Id'].nunique()} users")
print(f"📊 Hourly Data: {hourly_activity.shape[0]} rows, {hourly_activity.shape[1]} columns, {hourly_activity['Id'].nunique()} users")
print(f"📅 Date Range: {merged_data['Date'].min()} to {merged_data['Date'].max()}")

# Check for any missing values (should be 0)
print(f"\n✅ Missing values in merged_data: {merged_data.isnull().sum().sum()}")
print(f"✅ Missing values in hourly_activity: {hourly_activity.isnull().sum().sum()}")
```

    ============================================================
    BELLABEAT CASE STUDY - ANALYSIS PHASE
    ============================================================
    
    📊 Daily Data: 181 rows, 24 columns, 12 users
    📊 Hourly Data: 22099 rows, 6 columns, 33 users
    📅 Date Range: 2016-04-12 00:00:00 to 2016-05-12 00:00:00
    
    ✅ Missing values in merged_data: 0
    ✅ Missing values in hourly_activity: 0
    

#### What this tells me:

* I have 181 daily records from 12 users

* I have 22,099 hourly records from 33 users

* The data covers exactly 31 days (April 12 - May 12, 2016)

* There are no missing values in either dataset (data is clean!)

### 4.2: Daily Data Analysis
#### 4.2.1: Summary Statistics


```python
# ==========================================
# 2. DAILY DATA ANALYSIS
# ==========================================

print("\n" + "="*60)
print("SECTION 1: DAILY DATA ANALYSIS")
print("="*60)

# Sleep Statistics
print("\n💤 SLEEP STATISTICS:")

# Calculate sleep stats
avg_sleep_min = merged_data['TotalMinutesAsleep'].mean()
avg_sleep_hours = avg_sleep_min / 60
min_sleep = merged_data['TotalMinutesAsleep'].min()
max_sleep = merged_data['TotalMinutesAsleep'].max()
avg_efficiency = merged_data['SleepEfficiency'].mean()

sleep_stats = pd.DataFrame({
    'Metric': ['Average Sleep (minutes)', 'Average Sleep (hours)', 
               'Minimum Sleep (minutes)', 'Maximum Sleep (minutes)',
               'Average Sleep Efficiency (%)'],
    'Value': [avg_sleep_min, avg_sleep_hours, min_sleep, max_sleep, avg_efficiency]
})
print(sleep_stats.to_string(index=False))

# Activity Statistics
print("\n🏃 ACTIVITY STATISTICS:")

avg_steps = merged_data['TotalSteps'].mean()
avg_active = merged_data['TotalActiveMinutes'].mean()
avg_sedentary = merged_data['SedentaryMinutes'].mean()
avg_calories = merged_data['Calories'].mean()
avg_sedentary_pct = merged_data['SedentaryPercentage'].mean()

activity_stats = pd.DataFrame({
    'Metric': ['Average Steps', 'Average Active Minutes', 
               'Average Sedentary Minutes', 'Average Calories Burned',
               'Average Sedentary Percentage (%)'],
    'Value': [avg_steps, avg_active, avg_sedentary, avg_calories, avg_sedentary_pct]
})
print(activity_stats.to_string(index=False))

# Heart Rate Statistics
print("\n❤️ HEART RATE STATISTICS:")

avg_hr = merged_data['avg_heart_rate'].mean()
min_hr = merged_data['avg_heart_rate'].min()
max_hr = merged_data['avg_heart_rate'].max()

hr_stats = pd.DataFrame({
    'Metric': ['Average Heart Rate (bpm)', 'Minimum Heart Rate (bpm)', 
               'Maximum Heart Rate (bpm)'],
    'Value': [avg_hr, min_hr, max_hr]
})
print(hr_stats.to_string(index=False))
```

    
    ============================================================
    SECTION 1: DAILY DATA ANALYSIS
    ============================================================
    
    💤 SLEEP STATISTICS:
                          Metric      Value
         Average Sleep (minutes) 426.248619
           Average Sleep (hours)   7.104144
         Minimum Sleep (minutes)  58.000000
         Maximum Sleep (minutes) 775.000000
    Average Sleep Efficiency (%)  93.819783
    
    🏃 ACTIVITY STATISTICS:
                              Metric       Value
                       Average Steps 8521.613260
              Average Active Minutes  273.237569
           Average Sedentary Minutes  701.972376
             Average Calories Burned 2466.585635
    Average Sedentary Percentage (%)   71.262996
    
    ❤️ HEART RATE STATISTICS:
                      Metric      Value
    Average Heart Rate (bpm)  73.684703
    Minimum Heart Rate (bpm)  59.377175
    Maximum Heart Rate (bpm) 104.871472
    

#### 4.2.2: Sleep Quality Distribution


```python
 # ==========================================
# 2.2 SLEEP QUALITY DISTRIBUTION
# ==========================================

# Create sleep categories
def categorize_sleep(minutes):
    if minutes < 420:
        return 'Below Recommended (<7 hrs)'
    elif minutes <= 540:
        return 'Recommended (7-9 hrs)'
    else:
        return 'Above Recommended (>9 hrs)'

merged_data['SleepCategory'] = merged_data['TotalMinutesAsleep'].apply(categorize_sleep)

# Count distribution
sleep_dist = merged_data['SleepCategory'].value_counts().reset_index()
sleep_dist.columns = ['Sleep Category', 'Count']
sleep_dist['Percentage'] = (sleep_dist['Count'] / sleep_dist['Count'].sum() * 100).round(1)

print("\n📊 SLEEP CATEGORY DISTRIBUTION:")
print(sleep_dist.to_string(index=False))

# Calculate key metrics
below_rec = (merged_data['TotalMinutesAsleep'] < 420).sum()
below_rec_pct = below_rec / len(merged_data) * 100
print(f"\n⚠️ {below_rec_pct:.1f}% of days have less than 7 hours of sleep")
print(f"📊 Average sleep efficiency: {avg_efficiency:.1f}%")

# Sleep efficiency categories
def categorize_efficiency(eff):
    if eff < 70:
        return 'Poor (<70%)'
    elif eff < 85:
        return 'Good (70-85%)'
    else:
        return 'Excellent (>85%)'

merged_data['EfficiencyCategory'] = merged_data['SleepEfficiency'].apply(categorize_efficiency)
eff_dist = merged_data['EfficiencyCategory'].value_counts().reset_index()
eff_dist.columns = ['Efficiency Category', 'Count']
eff_dist['Percentage'] = (eff_dist['Count'] / eff_dist['Count'].sum() * 100).round(1)

print("\n📊 SLEEP EFFICIENCY DISTRIBUTION:")
print(eff_dist.to_string(index=False))
```

    
    📊 SLEEP CATEGORY DISTRIBUTION:
                Sleep Category  Count  Percentage
         Recommended (7-9 hrs)     90        49.7
    Below Recommended (<7 hrs)     71        39.2
    Above Recommended (>9 hrs)     20        11.0
    
    ⚠️ 39.2% of days have less than 7 hours of sleep
    📊 Average sleep efficiency: 93.8%
    
    📊 SLEEP EFFICIENCY DISTRIBUTION:
    Efficiency Category  Count  Percentage
       Excellent (>85%)    181       100.0
    

#### 4.2.3: Activity Level Distribution


```python
# ==========================================
# 2.3 ACTIVITY LEVEL DISTRIBUTION
# ==========================================

# Create step categories
def categorize_steps(steps):
    if steps < 5000:
        return 'Sedentary (<5,000)'
    elif steps < 10000:
        return 'Low Activity (5,000-10,000)'
    elif steps < 15000:
        return 'Active (10,000-15,000)'
    else:
        return 'Very Active (>15,000)'

merged_data['StepCategory'] = merged_data['TotalSteps'].apply(categorize_steps)

step_dist = merged_data['StepCategory'].value_counts().reset_index()
step_dist.columns = ['Step Category', 'Count']
step_dist['Percentage'] = (step_dist['Count'] / step_dist['Count'].sum() * 100).round(1)

print("\n📊 STEP CATEGORY DISTRIBUTION:")
print(step_dist.to_string(index=False))

# Calculate 10k target
meets_10k = (merged_data['TotalSteps'] >= 10000).sum()
meets_10k_pct = meets_10k / len(merged_data) * 100
print(f"\n🎯 {meets_10k_pct:.1f}% of days meet the 10,000 step target")

# Activity breakdown
print("\n📊 AVERAGE DAILY ACTIVITY BREAKDOWN (minutes):")
activity_breakdown = pd.DataFrame({
    'Activity Level': ['Very Active', 'Fairly Active', 'Lightly Active', 'Sedentary'],
    'Average Minutes': [
        merged_data['VeryActiveMinutes'].mean(),
        merged_data['FairlyActiveMinutes'].mean(),
        merged_data['LightlyActiveMinutes'].mean(),
        merged_data['SedentaryMinutes'].mean()
    ]
})
print(activity_breakdown.to_string(index=False))
```

    
    📊 STEP CATEGORY DISTRIBUTION:
                  Step Category  Count  Percentage
         Active (10,000-15,000)     67        37.0
    Low Activity (5,000-10,000)     64        35.4
             Sedentary (<5,000)     39        21.5
          Very Active (>15,000)     11         6.1
    
    🎯 43.1% of days meet the 10,000 step target
    
    📊 AVERAGE DAILY ACTIVITY BREAKDOWN (minutes):
    Activity Level  Average Minutes
       Very Active        27.994475
     Fairly Active        16.596685
    Lightly Active       228.646409
         Sedentary       701.972376
    

#### 4.2.4: Heart Rate Distribution


```python
# ==========================================
# 2.4 HEART RATE DISTRIBUTION
# ==========================================

# Create heart rate categories
def categorize_hr(hr):
    if hr < 60:
        return 'Low HR (<60 bpm)'
    elif hr < 70:
        return 'Below Average (60-69 bpm)'
    elif hr < 80:
        return 'Average (70-79 bpm)'
    else:
        return 'Above Average (80+ bpm)'

merged_data['HRCategory'] = merged_data['avg_heart_rate'].apply(categorize_hr)

hr_dist = merged_data['HRCategory'].value_counts().reset_index()
hr_dist.columns = ['Heart Rate Category', 'Count']
hr_dist['Percentage'] = (hr_dist['Count'] / hr_dist['Count'].sum() * 100).round(1)

print("\n📊 HEART RATE CATEGORY DISTRIBUTION:")
print(hr_dist.to_string(index=False))
```

    
    📊 HEART RATE CATEGORY DISTRIBUTION:
          Heart Rate Category  Count  Percentage
          Average (70-79 bpm)     75        41.4
    Below Average (60-69 bpm)     61        33.7
      Above Average (80+ bpm)     42        23.2
             Low HR (<60 bpm)      3         1.7
    

#### 4.2.5: Day of Week Patterns


```python
# ==========================================
# 2.5 DAY OF WEEK PATTERNS
# ==========================================

# Ensure DayOfWeek exists
if 'DayOfWeek' not in merged_data.columns:
    merged_data['DayOfWeek'] = merged_data['Date'].dt.day_name()

weekday_order = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 
                 'Friday', 'Saturday', 'Sunday']

# Sleep by day
sleep_by_day = merged_data.groupby('DayOfWeek')['TotalMinutesAsleep'].mean().reindex(weekday_order).reset_index()
sleep_by_day.columns = ['DayOfWeek', 'AvgSleepMinutes']
sleep_by_day['AvgSleepHours'] = (sleep_by_day['AvgSleepMinutes'] / 60).round(1)

print("\n📅 AVERAGE SLEEP BY DAY OF WEEK:")
print(sleep_by_day.to_string(index=False))

# Steps by day
steps_by_day = merged_data.groupby('DayOfWeek')['TotalSteps'].mean().reindex(weekday_order).reset_index()
steps_by_day.columns = ['DayOfWeek', 'AvgSteps']

print("\n📅 AVERAGE STEPS BY DAY OF WEEK:")
print(steps_by_day.to_string(index=False))

# Heart rate by day
hr_by_day = merged_data.groupby('DayOfWeek')['avg_heart_rate'].mean().reindex(weekday_order).reset_index()
hr_by_day.columns = ['DayOfWeek', 'AvgHeartRate']

print("\n📅 AVERAGE HEART RATE BY DAY OF WEEK:")
print(hr_by_day.to_string(index=False))

# Best and worst days
best_sleep = sleep_by_day.loc[sleep_by_day['AvgSleepHours'].idxmax()]
worst_sleep = sleep_by_day.loc[sleep_by_day['AvgSleepHours'].idxmin()]

print(f"\n🌟 Best sleep day: {best_sleep['DayOfWeek']} ({best_sleep['AvgSleepHours']:.1f} hours)")
print(f"🌙 Worst sleep day: {worst_sleep['DayOfWeek']} ({worst_sleep['AvgSleepHours']:.1f} hours)")

best_step = steps_by_day.loc[steps_by_day['AvgSteps'].idxmax()]
worst_step = steps_by_day.loc[steps_by_day['AvgSteps'].idxmin()]

print(f"🌟 Most active day: {best_step['DayOfWeek']} ({best_step['AvgSteps']:.0f} steps)")
print(f"🌙 Least active day: {worst_step['DayOfWeek']} ({worst_step['AvgSteps']:.0f} steps)")
```

    
    📅 AVERAGE SLEEP BY DAY OF WEEK:
    DayOfWeek  AvgSleepMinutes  AvgSleepHours
       Monday       431.590909            7.2
      Tuesday       411.037037            6.9
    Wednesday       461.655172            7.7
     Thursday       405.428571            6.8
       Friday       403.800000            6.7
     Saturday       420.565217            7.0
       Sunday       446.296296            7.4
    
    📅 AVERAGE STEPS BY DAY OF WEEK:
    DayOfWeek    AvgSteps
       Monday 8814.000000
      Tuesday 9612.222222
    Wednesday 7319.068966
     Thursday 9331.678571
       Friday 8061.640000
     Saturday 9639.130435
       Sunday 7118.259259
    
    📅 AVERAGE HEART RATE BY DAY OF WEEK:
    DayOfWeek  AvgHeartRate
       Monday     75.489577
      Tuesday     74.019296
    Wednesday     70.364782
     Thursday     74.107888
       Friday     73.290274
     Saturday     75.734668
       Sunday     73.625399
    
    🌟 Best sleep day: Wednesday (7.7 hours)
    🌙 Worst sleep day: Friday (6.7 hours)
    🌟 Most active day: Saturday (9639 steps)
    🌙 Least active day: Sunday (7118 steps)
    

#### 4.2.6: Correlation Analysis


```python
# ==========================================
# 2.6 CORRELATION ANALYSIS
# ==========================================

# Select key columns for correlation
correlation_cols = [
    'TotalSteps', 
    'TotalActiveMinutes', 
    'SedentaryMinutes',
    'Calories', 
    'TotalMinutesAsleep', 
    'SleepEfficiency', 
    'avg_heart_rate'
]

# Calculate correlation matrix
correlation_matrix = merged_data[correlation_cols].corr()

print("\n📊 CORRELATION MATRIX:")
print("(Values close to 1 = strong positive relationship)")
print("(Values close to -1 = strong negative relationship)")
print("(Values near 0 = no relationship)")
print("\n" + correlation_matrix.round(3).to_string())

# Extract key correlations
print("\n🔗 KEY RELATIONSHIPS:")

# Steps vs Calories
steps_cal = merged_data['TotalSteps'].corr(merged_data['Calories'])
print(f"Steps ↔ Calories: {steps_cal:.3f}")

# Active Minutes vs Calories
active_cal = merged_data['TotalActiveMinutes'].corr(merged_data['Calories'])
print(f"Active Minutes ↔ Calories: {active_cal:.3f}")

# Sedentary vs Calories
sed_cal = merged_data['SedentaryMinutes'].corr(merged_data['Calories'])
print(f"Sedentary Minutes ↔ Calories: {sed_cal:.3f}")

# Sleep vs Heart Rate
sleep_hr = merged_data['TotalMinutesAsleep'].corr(merged_data['avg_heart_rate'])
print(f"Sleep Duration ↔ Heart Rate: {sleep_hr:.3f}")

# Sleep Efficiency vs Heart Rate
eff_hr = merged_data['SleepEfficiency'].corr(merged_data['avg_heart_rate'])
print(f"Sleep Efficiency ↔ Heart Rate: {eff_hr:.3f}")

# Steps vs Sleep
steps_sleep = merged_data['TotalSteps'].corr(merged_data['TotalMinutesAsleep'])
print(f"Steps ↔ Sleep Duration: {steps_sleep:.3f}")
```

    
    📊 CORRELATION MATRIX:
    (Values close to 1 = strong positive relationship)
    (Values close to -1 = strong negative relationship)
    (Values near 0 = no relationship)
    
                        TotalSteps  TotalActiveMinutes  SedentaryMinutes  Calories  TotalMinutesAsleep  SleepEfficiency  avg_heart_rate
    TotalSteps               1.000               0.771            -0.190     0.493              -0.082           -0.006           0.154
    TotalActiveMinutes       0.771               1.000            -0.283     0.488              -0.046            0.027           0.387
    SedentaryMinutes        -0.190              -0.283             1.000     0.053              -0.622            0.097           0.080
    Calories                 0.493               0.488             0.053     1.000              -0.127            0.106          -0.009
    TotalMinutesAsleep      -0.082              -0.046            -0.622    -0.127               1.000            0.011          -0.252
    SleepEfficiency         -0.006               0.027             0.097     0.106               0.011            1.000           0.139
    avg_heart_rate           0.154               0.387             0.080    -0.009              -0.252            0.139           1.000
    
    🔗 KEY RELATIONSHIPS:
    Steps ↔ Calories: 0.493
    Active Minutes ↔ Calories: 0.488
    Sedentary Minutes ↔ Calories: 0.053
    Sleep Duration ↔ Heart Rate: -0.252
    Sleep Efficiency ↔ Heart Rate: 0.139
    Steps ↔ Sleep Duration: -0.082
    

#### 4.2.7: User Segmentation


```python
# ==========================================
# 2.7 USER SEGMENTATION
# ==========================================

# Create user profiles (average per user)
user_profiles = merged_data.groupby('Id').agg({
    'TotalSteps': 'mean',
    'TotalActiveMinutes': 'mean',
    'TotalMinutesAsleep': 'mean',
    'SleepEfficiency': 'mean',
    'avg_heart_rate': 'mean',
    'Calories': 'mean',
    'SedentaryMinutes': 'mean'
}).reset_index()

print(f"\n👥 User Profiles Created: {len(user_profiles)} users")

# Activity Level Segmentation
def get_activity_level(steps):
    if steps < 5000:
        return 'Sedentary'
    elif steps < 10000:
        return 'Lightly Active'
    elif steps < 15000:
        return 'Very Active'
    

user_profiles['ActivityLevel'] = user_profiles['TotalSteps'].apply(get_activity_level)

# Sleep Quality Segmentation
def get_sleep_quality(efficiency):
    if efficiency < 70:
        return 'Poor'
    elif efficiency < 85:
        return 'Good'
    else:
        return 'Excellent'

user_profiles['SleepQuality'] = user_profiles['SleepEfficiency'].apply(get_sleep_quality)

# Heart Rate Category
def get_hr_category(hr):
    if hr < 60:
        return 'Low HR'
    elif hr < 70:
        return 'Below Average'
    elif hr < 80:
        return 'Average'
    else:
        return 'Above Average'

user_profiles['HRCategory'] = user_profiles['avg_heart_rate'].apply(get_hr_category)

print("\n📊 USER SEGMENTATION SUMMARY:")

# Activity Level Distribution
activity_segments = user_profiles['ActivityLevel'].value_counts().reset_index()
activity_segments.columns = ['Activity Level', 'Number of Users']
print("\n🏃 BY ACTIVITY LEVEL:")
print(activity_segments.to_string(index=False))

# Sleep Quality Distribution
sleep_segments = user_profiles['SleepQuality'].value_counts().reset_index()
sleep_segments.columns = ['Sleep Quality', 'Number of Users']
print("\n💤 BY SLEEP QUALITY:")
print(sleep_segments.to_string(index=False))

# Heart Rate Distribution
hr_segments = user_profiles['HRCategory'].value_counts().reset_index()
hr_segments.columns = ['Heart Rate Category', 'Number of Users']
print("\n❤️ BY HEART RATE CATEGORY:")
print(hr_segments.to_string(index=False))

# Cross-segmentation
cross_seg = user_profiles.groupby(['ActivityLevel', 'SleepQuality']).size().reset_index()
cross_seg.columns = ['Activity Level', 'Sleep Quality', 'Count']
print("\n🔀 CROSS-SEGMENTATION (Activity × Sleep):")
print(cross_seg.to_string(index=False))

# User profile summary
print("\n📊 USER PROFILE SUMMARY STATISTICS:")
print(user_profiles[['TotalSteps', 'TotalMinutesAsleep', 'SleepEfficiency', 'avg_heart_rate']].describe())
```

    
    👥 User Profiles Created: 12 users
    
    📊 USER SEGMENTATION SUMMARY:
    
    🏃 BY ACTIVITY LEVEL:
    Activity Level  Number of Users
    Lightly Active                9
         Sedentary                2
       Very Active                1
    
    💤 BY SLEEP QUALITY:
    Sleep Quality  Number of Users
        Excellent               12
    
    ❤️ BY HEART RATE CATEGORY:
    Heart Rate Category  Number of Users
          Above Average                6
                Average                3
          Below Average                3
    
    🔀 CROSS-SEGMENTATION (Activity × Sleep):
    Activity Level Sleep Quality  Count
    Lightly Active     Excellent      9
         Sedentary     Excellent      2
       Very Active     Excellent      1
    
    📊 USER PROFILE SUMMARY STATISTICS:
             TotalSteps  TotalMinutesAsleep  SleepEfficiency  avg_heart_rate
    count     12.000000           12.000000        12.000000       12.000000
    mean    7415.988487          374.691158        93.686385       77.377463
    std     2450.507699          137.442378         1.869813        7.416402
    min     3443.266667           68.500000        90.712766       65.937784
    25%     5883.500000          349.593750        92.657000       71.410374
    50%     8336.100000          433.833333        93.970467       79.205437
    75%     8932.894231          451.870968        94.970616       82.265928
    max    11034.347826          496.250000        96.148725       87.632634
    

#### Summary

* 12 user profiles were created by grouping users by their average daily steps, sleep efficiency, and heart rate.

* Users were classified into four activity levels based on average daily steps: Sedentary, Lightly Active and Very Active.

* Users were classified into four heart rate levels based on average daily heart rate: Low HR, Below Average, Average and Above Average.

* Uswes were also classified into three sleep quality levels based on average sleep efficiency: Poor, Good and Exellent.
  
* This segmentation enables comparative analysis of sleep and heart rate patterns across different activity groups.

The profiles will serve as the foundation for all **visualizations** in this analysis.

### 4.3: Hourly Analysis

#### 4.3.1 Peak Hours


```python
# ==========================================
# 3.1 PEAK HOURS ANALYSIS
# ==========================================

hourly_summary = hourly_activity.groupby('Hour').agg({
    'StepTotal': 'mean',
    'Calories': 'mean',
    'TotalIntensity': 'mean'
}).reset_index()

peak_step = hourly_summary.loc[hourly_summary['StepTotal'].idxmax()]

print("\n⏰ PEAK ACTIVITY HOURS:")
print(f"Peak Activity: {int(peak_step['Hour'])}:00 ({peak_step['StepTotal']:.0f} avg steps)")

# Top 3 and bottom 3 hours
top_3 = hourly_summary.nlargest(3, 'StepTotal')[['Hour', 'StepTotal']]
bottom_3 = hourly_summary.nsmallest(3, 'StepTotal')[['Hour', 'StepTotal']]

print("\n🔆 TOP 3 MOST ACTIVE HOURS:")
for _, row in top_3.iterrows():
    print(f"  {int(row['Hour'])}:00 - {row['StepTotal']:.0f} steps")

print("\n🌙 TOP 3 LEAST ACTIVE HOURS:")
for _, row in bottom_3.iterrows():
    print(f"  {int(row['Hour'])}:00 - {row['StepTotal']:.0f} steps")
```

    
    ⏰ PEAK ACTIVITY HOURS:
    Peak Activity: 18:00 (599 avg steps)
    
    🔆 TOP 3 MOST ACTIVE HOURS:
      18:00 - 599 steps
      19:00 - 583 steps
      17:00 - 550 steps
    
    🌙 TOP 3 LEAST ACTIVE HOURS:
      3:00 - 6 steps
      4:00 - 13 steps
      2:00 - 17 steps
    

#### Summary

* Sorted hours by StepTotal in **descending** order to identify most active hours.
* Sorted hours by StepTotal in **ascending** order to identify least active hours.


#### 4.3.2: Time Perion Analysis 


```python
# ==========================================
# 3.2 TIME PERIOD ANALYSIS
# ==========================================

def get_time_period(hour):
    if 5 <= hour < 12:
        return 'Morning (5am-12pm)'
    elif 12 <= hour < 17:
        return 'Afternoon (12pm-5pm)'
    elif 17 <= hour < 21:
        return 'Evening (5pm-9pm)'
    else:
        return 'Night (9pm-5am)'

hourly_activity['TimePeriod'] = hourly_activity['Hour'].apply(get_time_period)

time_period_summary = hourly_activity.groupby('TimePeriod').agg({
    'StepTotal': 'mean'
}).reset_index()

period_order = ['Morning (5am-12pm)', 'Afternoon (12pm-5pm)', 
                'Evening (5pm-9pm)', 'Night (9pm-5am)']
time_period_summary['TimePeriod'] = pd.Categorical(
    time_period_summary['TimePeriod'], 
    categories=period_order, 
    ordered=True
)
time_period_summary = time_period_summary.sort_values('TimePeriod')

total_steps = time_period_summary['StepTotal'].sum()
time_period_summary['Percentage'] = (time_period_summary['StepTotal'] / total_steps * 100).round(1)

print("\n⏰ ACTIVITY BY TIME PERIOD:")
print(time_period_summary.to_string(index=False))
```

    
    ⏰ ACTIVITY BY TIME PERIOD:
              TimePeriod  StepTotal  Percentage
      Morning (5am-12pm) 332.379914        22.8
    Afternoon (12pm-5pm) 506.171391        34.8
       Evening (5pm-9pm) 521.674669        35.9
         Night (9pm-5am)  94.760336         6.5
    

#### Summary

* Grouped hourly step data into four defined time periods:
  - **Morning** (5am – 12pm)
  - **Afternoon** (12pm – 5pm)
  - **Evening** (5pm – 9pm)
  - **Night** (9pm – 5am)
    

* Calculated total steps for each time period by summing `StepTotal` values within the respective hourly buckets.

* Computed the percentage contribution of each period to overall daily steps using:
  ```python
  time_period_summary[Percentage] = (time_period_summary[StepTotal] / total_steps) * 100

The time period breakdown is multi-day aggregation, not a single day's distribution. The percentages (22.8%, 34.8%, etc.) show how steps are typically distributed across the day, not daily totals.

## 5: SHARE PHASE
#### 5.1: Data Exportation
The Required datasets would be exported for visualizations on Microsoft PowerBI


```python
# ==========================================
# EXPORT DATA FOR VISUALIZATIONS
# ==========================================

print("\n" + "="*60)
print("EXPORTING DATA FOR VISUALIZATIONS")
print("="*60)

user_profiles.to_csv('fitbit_user_profiles_for_visualizations.csv', index=False)
print("✅ fitbit_user_profiles_for_visualizations.csv")

hourly_summary.to_csv('fitbit_hourly_summary_for_visualizations.csv', index=False)
print("✅ fitbit_hourly_summary_for_visualizations.csv")

sleep_by_day.to_csv('fitbit_sleep_by_day.csv', index=False)
print("✅ fitbit_sleep_by_day.csv")

steps_by_day.to_csv('fitbit_steps_by_day.csv', index=False)
print("✅ fitbit_steps_by_day.csv")

correlation_matrix.to_csv('fitbit_correlation_matrix.csv')
print("✅ fitbit_correlation_matrix.csv")

time_period_summary.to_csv('fitbit_time_period_summary.csv', index=False)
print("✅ fitbit_time_period_summary.csv")

cross_seg.to_csv('fitbit_cross_segmentation.csv', index=False)
print("✅ fitbit_cross_segmentation.csv")

print("\n✅ ALL DATA EXPORTED SUCCESSFULLY!")
```

    
    ============================================================
    EXPORTING DATA FOR VISUALIZATIONS
    ============================================================
    ✅ fitbit_user_profiles_for_visualizations.csv
    ✅ fitbit_hourly_summary_for_visualizations.csv
    ✅ fitbit_sleep_by_day.csv
    ✅ fitbit_steps_by_day.csv
    ✅ fitbit_correlation_matrix.csv
    ✅ fitbit_time_period_summary.csv
    ✅ fitbit_cross_segmentation.csv
    
    ✅ ALL DATA EXPORTED SUCCESSFULLY!
    

## 6:ACT PHASE
#### 6.1: Insights and Marketing Recommendations 

#### How Consumers Are Currently Using Their Smart Devices

**Activity: Active Enough, But Dangerously Sedentary**

* Users average 8,561 steps per day — comfortably above the commonly cited 8K benchmark.

* However, they spend 789.78 minutes (~13.1 hours) sedentary — roughly 71% of their tracked day.

* The correlation matrix confirms that steps and active minutes are very well linked (0.77) — meaning users who move, move consistently, but        most simply aren't moving enough throughout the day.

* Evening (5pm–9pm) is the peak activity window, followed by afternoon. Morning activity is notably low.

**Sleep: Good Quality, Inconsistent Quantity**
Average sleep is 7.10 hours — right at the borderline of the recommended 7–9 hours.

* Sleep efficiency is 93.69%, with 100% of tracked days falling in the "Excellent" category (>85%) — meaning when users sleep, they sleep deeply and uninterrupted.

* However, 43% of days fall below 7 hours — a significant portion of the time, users are sleep-deprived.

* Sleep duration peaks on Wednesdays with Sundays and Mondays being significantly higher than the rest, suggesting a Mid-week spike, weekend        catch-up pattern followed by gradual sleep loss during the workweek.

**Heart Rate: Mixed Cardiovascular Baseline**

* Average heart rate is 77.38 bpm — within normal range but on the higher side.

* 50% of users have an above-average heart rate, while the other 50% are evenly split between average and below average.


**What This Means for Bellabeat Customers**

 Bellabeat's target audience — health-conscious women — likely mirrors these patterns:

* They are time-poor and desk-bound, relying on evening movement to hit activity goals.

* They value sleep quality but struggle to protect sleep duration during busy workweeks.

* They are responsive to recovery metrics (high sleep efficiency proves this).

* They need low-time-commitment, high-impact health solutions — not more pressure to "do more."

**High-Level Marketing Recommendations for Bellabeat**

1. Reposition the Bellabeat App as a "Recovery & Micro-Habit Coach"
Why: Users are active enough in steps but severely sedentary and inconsistent with sleep. The market doesn't need another step counter — it needs a tool that helps busy women integrate health into fragmented days.

How:

* Shift messaging from "hit 10,000 steps" to "move more, sit less, sleep better."

* Highlight the Bellabeat App's stress, sleep, and activity tracking as a holistic recovery system.

* Emphasize micro-habits — **5-minute desk stretches**, **hourly movement reminders**, **evening wind-down prompts**.

2. Launch a "Desktop Detox" Campaign
Why: 71% of the day is sedentary — this is the single biggest health risk in the data.

How:

* Market the Bellabeat App's inactivity alerts and movement reminders.

* Create content around "Micro-Workouts for Desk Jobs" — short, app-guided sessions that fit into a workday.

* Position sedentary reduction as a stress-management tool, not just a fitness goal — aligning with Bellabeat's holistic brand.

3. Introduce a "Weekly Sleep Consistency" Campaign

Why: Sleep efficiency is excellent (93.69%), but duration is inconsistent across the week. Saturday, Sunday, Monday and Wednesday meet the 7+ hour recommendation (with Wednesday peaking highest at ~7.70 hrs), while Tuesday, Thursday and Friday, all fall below 7 hours.

How:

* Market the Bellabeat App as a sleep consistency coach, not just a sleep tracker.

* Send Tuesday, Thursday and Friday evening notifications encouraging earlier wind-downs — targeting the exact days sleep drops below recommended   levels.

* Promote "Midweek Momentum" content on Wednesdays to capitalize on the weekly sleep peak and reinforce healthy routines heading into the rest of   the week.


4. Capitalize on the Evening Activity Peak
Why: Users are most active between 5pm and 9pm.

How:

* Time app notifications, social media ads, and email campaigns for the 5pm–9pm window.

* Create evening movement challenges and streaks in the Bellabeat App.

* Highlight calorie burn and active minutes in evening messaging — since calories correlate strongly with both steps and active minutes.

5. Use Heart Rate Data to Promote Holistic Health Tracking

Why: Average heart rate across users is 77.38 bpm, with 50% of users falling into the above-average category, while the remaining 50% is evenly split between average and below-average. This suggests a mixed cardiovascular baseline across the user base — an opportunity to position heart rate as a wellness indicator, not just a workout metric.

How:

* Position the Bellabeat App's heart rate monitoring as a way to understand stress, recovery, and cardiovascular trends — not just workout intensity.

* Market to users who want to improve heart health without high-intensity exercise — walking, yoga, and stress reduction all count.

  
**Final Stakeholder Takeaway**
Consumers are not failing at fitness — they are time-poor, desk-bound, and sleep-inconsistent, but they do achieve high-quality sleep when they get it. Bellabeat's opportunity is to stop competing on step counts and instead own the recovery and micro-habit space. By positioning the Bellabeat App as a holistic coach that helps busy women move more throughout the day and protect their sleep during the week, Bellabeat can differentiate itself in a saturated market and deepen engagement with its core audience.




