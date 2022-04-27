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

(Majority of cleaning done in Microsoft Excel, prior to reading data sets into RStudio. Code examples will be included for any cleaning completed through Rstudio.)

- Changed format of Id from numeric string to 'user_1:33'

- Removed rows containing missing values for TotalSteps and TotalDistance in dailyActivity_merged data set (appears as though user left running but did not use.)

- Dropped rows with missing values in hourlyIntensities_merged, hourlySteps_merged, minuteCaloriesNarrow_merged, and minuteStepsNarrow_merged.

- Removed rows in sleepDay_merged for times less than 2 hours in TotalTimeinBed, I do not consider this to be normal sleeping hours and thus may skew trends in our analysis for a normal night’s sleep.

- dailyActivity_merged: removed outliers for user_2 on 5/1/2016 and user_33 on 4/30/2016 because of VeryActiveDistance greater than 20miles. After comparing VeryActiveDistance to VeryActiveMinutes, it does not make sense unless running at a very fast pace.
       - This datum could be due to other factors such as biking, roller blading, or driving          a vehicle.

- Removed sedentaryactivedistance from dailyintensities_merged data set due to redundancy.

## Summary of Analysis
After reviewing these data sets I have discovered three major trends. First is from the "sleepday_merged data set." Here, I analyzed the average hours of sleep each user is getting per night, from March 12 through April 12. After dropping outliers and analyzing the data it is apparent that users are getting between 6 to 8 hours of sleep. My second analyzation was of the "heartrate_seconds_merged" and "hourlyntensity_merged" data sets. After analyzing data for user 6 on 4/12/16, it is noticeable the effect that average intensity has on heart rate. These two variables are strongly correlated with a correlation coefficient of **0.878**. My last analysis was of weight log information. Trends in this data set show that many users are not logging their weight information. 

# Visualizations and Key Findings

### Sleep Patterns

This visualization represents sleep patterns of users from April 2016 to May of 2016. I have decided to drop data from user 4 and user 18 due to unrealistic sleep times. 22 of 33 users were included in this data set due to lack of input data.

My first analysis will be of sleepDay_merged data. I want to analyze normal amount of sleep per user.

![Alt Text](/cloud/project/data_visualizations/Avg_hours_asleepFINAL.jpeg)

read data
```{r}
my_data <- read.csv("CopyOfsleepDay_mergedcleaned.csv")
```
convert totalminutesasleep to totalhoursasleep, apply TotalHoursAsleep to my_data
```{r}
TotalHoursAsleep <- my_data$TotalMinutesAsleep/60 
my_data$TotalHoursAsleep <- TotalHoursAsleep
```
mean hours asleep for each user, rename TotalHoursAsleep to avghoursasleep
```{r}
my_data2 <- aggregate(TotalHoursAsleep ~ Id, my_data, mean)
my_data2 <- my_data2 %>% 
  rename(
    avg_hours_asleep = TotalHoursAsleep)
```
rename all numeric Id values to user_xx and create factor level
```{r}
user_id <- c("user_1", "user_3", "user_4", "user_5", "user_7", "user_9", "user_12","user_13","user_15","user_16",
             "user_17","user_18","user_19","user_20","user_21","user_22","user_24","user_25","user_27","user_28","user_30", "user_32")

lvls2 <- c("user_1", "user_3", "user_4", "user_5", "user_7", "user_9", "user_12","user_13","user_15","user_16",
                      "user_17","user_18","user_19","user_20","user_21","user_22","user_24","user_25","user_27","user_28","user_30", "user_32")
```
assign user_id variable to my_data2, drop user 4 and user 18
```{r}
my_data2$user_id <- user_id
my_data3 <- my_data2[-c(12, 3),]
```
assign factor levels to user_id
```{r}
my_data3$user_id <- factor(my_data3$user_id, levels = lvls2)
```
plot
```{r, fig.show='hide'}
ggplot(data=my_data3, aes(x=user_id,y=avg_hours_asleep, group=1)) +
  geom_point() +
  geom_smooth(formula = y ~ x, method = "lm") +
  theme(axis.text.x = element_text(angle = 45))
```

