# Google Data Analytics Professional Certificate Capstone Project #1
## BellaBeat
## Introduction
You are a junior data analyst working on the marketing analyst team at Bellabeat, a high-tech manufacturer of health-focused
products for women. Bellabeat is a successful small company, but they have the potential to become a larger player in the
global smart device market. Urška Sršen, cofounder and Chief Creative Officer of Bellabeat, believes that analyzing smart
device fitness data could help unlock new growth opportunities for the company. You have been asked to focus on one of
Bellabeat’s products and analyze smart device data to gain insight into how consumers are using their smart devices. The
insights you discover will then help guide marketing strategy for the company. You will present your analysis to the Bellabeat
executive team along with your high-level recommendations for Bellabeat’s marketing strategy.

## Business Task
Bellabeat has hired a data analyst to analyze smart device usage data in order to gain insight into how consumers use non-Bellabeat smart devices. The trends I discover in this data will influence marketing strategy for the Bellabeat app based on analyzing trends in data from users with smart devices unrelated to Bellabeat products. These insights can drive business decisions based on how to market the product, what features of the product to enhance or optimize, and what features to disable or ways to save money within the product line (least used features of the product based on trends in smart device data.) 

## Description of Data Sources
https://www.kaggle.com/datasets/arashnic/fitbit (FitBit Fitness Tracker Data) (CC0: Public Domain, dataset made available through Mobius): This Kaggle data set
contains personal fitness tracker from thirty fitbit users. Thirty eligible Fitbit users consented to the submission of
personal tracker data, including minute-level output for physical activity, heart rate, and sleep monitoring. It includes
information about daily activity, steps, and heart rate that can be used to explore users’ habits.

## Documented Cleaning Process
Changed format of Id from number string to “user _1:33”

Removed rows in dailyActivity_merged for missing data values (appears as though user left running but did not use.)
- user_1: date 5-12
- user_23: date 5-10
- user_29: date 4-30 
- user_31: day 5-12

Noticed rows of data with missing values in dailyActivity_merged at user_23: date 4/21, 4/23, 4/26, and 4/29.
Removed due to lack of data within all categories excluding calories and sedentary minutes.

Dropped rows with missing values in hourlyIntensities_merged, hourlySteps_merged, minuteCaloriesNarrow_merged, and minuteStepsNarrow_merged

Removed rows in sleepDay_merged for times less than 2 hours in TotalTimeinBed, I do not consider this to be normal sleeping hours and thus may skew trends in our analysis for a normal night’s sleep.

dailyActivity_merged: removed outlier for id 1624580081 on 5/1/2016 and Id 8877689391 on 4/30 because of VeryActiveDistance greater than 20miles. After comparing Distance to Minutes, it does not make sense unless running at a very fast pace ~sub 6 minute mile for user 887.
because of very active distance of 21 miles in 186 minutes. The user could be running a marathon at a strong pace 8.8min/mile however it is unlikely considering other days showed no signs of preparing for a marathon. This datum could be due to other factors such as biking or roller blading.  

Removed sedentaryactivedistance from dailyintensities_merged data set due to redundancy.

## Summary of Analysis
After formatting and reviewing these data sets, I decided to bring three points to the forefront. First is from the sleepday_merged data set. Here I analyzed the average hours of sleep each user is getting per night, from 4/12/2016 – 5/12/2016. I decided to drop user_4 and user_18 due to unrealistic sleep times (under 2 hours and over 12 hours averages.) After dropping outliers and analyzing the data it is apparent that users are getting between 6 to 8 hours of sleep on average, each night with a few users above or below those numbers. My second analyzation was of heart rate and average intensity data. After creating graphs and comparing data for user 6 on 4/12/16 it is noticeable the effect that intensity has on heart rate, these two variables are strongly correlated with a coefficient of 0.878. My last analysis was of weight log information. After reviewing this dataset I decided it was necessary to inform bellabeat that many users are not logging their weight information. I assume this is because of lack of knowledge, inability to use weight scales, or inconvenience to enter data. This is a point of strategy for bellabeat as they go forward in creating their products. Making weight log entry easier to maintain will be a key to success in their future product strategy. 

# Visualizations and Key Findings

My first analysis will be of sleepDay_merged data. I want to analyze normal amount of sleep per user.

![image](https://user-images.githubusercontent.com/103777815/163675104-b955c9a2-5603-4bf7-af80-f846fc952e04.png)

This is a visualization created In RStudio Cloud representing sleep patterns of users from our smart device data set. I have decided to drop data from user 4 and user 18 due to unrealistic sleep times.  [only 22/33 users included in this dataset.] 

Summary Statistics:
[1] "STATISTICAL SUMMARY of total hours asleep for three randomly selected users. 4/12/2016 - 5/11/2016"

user_13 

   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
  3.767   5.717   6.417   6.471   7.667   8.350 

user_17

   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
  5.367   6.054   6.850   6.783   7.342   8.367 


User_5

  Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
  2.767   4.933   6.633   6.950   7.917  12.500 

My second analyzation comes from heart rate data. I visualized the data from user 6 on 4/12/16 from 7AM to 8PM to show how his heart rate varied along with his average intensity. The graphs look similar indicating a strong relationship. This relationship is reinforced by a correlation coefficient of 0.878 measured between heartrate value and average intensity.
![image](https://user-images.githubusercontent.com/103777815/163675159-b6227eb9-e9be-402f-8627-a39f83b38176.png)
![image](https://user-images.githubusercontent.com/103777815/163675162-0f3e4a5d-fca9-46f6-98a8-695c9488c12f.png)

My third visualization is indicating a lack of data entry in weight log information. The number of users that logged weight information is very small, with many of them logging less than 5 times for the entire month. I am assuming this has to do with weight scale not being available, unknowledgeable on how to measure BMI, or inconvenience to enter data. 
![image](https://user-images.githubusercontent.com/103777815/163675205-add88d2c-65a3-4423-979a-dbcafde39665.png)

My last analyzation comes from daily activity merged data set measuring Activity levels and how they very throughout the month. As you can see from the graph, sedentary is the highest amount ranging from slightly above 500 minutes per day all the way up to 1400 minutes per day. Below this is Fairly Active Minutes and then Very active and lightly active. As you can see most of user 1’s time through out the month is spent being sedentary. Creating an alarm within the BellaBeat app when sedentary times raise over a certain level would be something to implement to promote healthiness within individuals. Or even creating a feature within the app that sets goals for very/fairly active minutes.

![image](https://user-images.githubusercontent.com/103777815/163675190-3da36496-71fa-4b3a-a21e-56f5b1c6ecb2.png)
![image](https://user-images.githubusercontent.com/103777815/163675195-9eb4c6ad-9acf-4d59-a9ba-2adedf3053b6.png)

## Recommendations based on Analysis

To influence sales and usage of the Bellabeat app the company will need to implement analyzations of sleep, heart rate, intensity, and similar data within the app. It will also benefit the company to find ways in which users can easily log weight data as this was a point of concern within these data sets. Lastly, alarms within the app should be created to alert users of their activity goals for the day.


