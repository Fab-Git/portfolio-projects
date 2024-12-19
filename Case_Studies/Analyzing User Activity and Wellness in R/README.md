# Bellabeat Wellness Device Case Study: Analyzing User Activity and Wellness Patterns

## Introduction
The **Bellabeat Wellness Device Case Study** explores user activity patterns, sleep behavior, and calorie expenditure to gain insights into wellness trends. This analysis helps **Bellabeat**, a wellness technology company, understand user behavior and enhance engagement through their products. Using data from Bellabeat devices, the study aims to identify actionable insights to guide product design and marketing strategies.

The study follows a structured 6-step framework:
1. **Ask**: Define objectives and business tasks.
2. **Prepare**: Collect, clean, and inspect data.
3. **Process**: Perform data aggregation and exploratory analysis.
4. **Analyze**: Uncover trends, patterns, and correlations.
5. **Share**: Visualize findings through dashboards.
6. **Act**: Recommend actionable steps for Bellabeat.

---

## 1. Ask
### Objective:
Analyze activity and wellness data from Bellabeat devices to understand user behavior and trends.

### Business Questions:
- What are the daily activity patterns of Bellabeat users?
- How do steps, calories, and sleep patterns vary across the week?
- Are there correlations between steps taken and calories burned?

---

## 2. Prepare
### Data Sources:
- Bellabeat wellness data, including metrics such as daily steps, calories burned, activity levels, and sleep duration.

### Data Preparation:
- Imported datasets using R libraries like `tidyverse` and `lubridate`.
- Inspected data for column names, data types, and sample records.
- Cleaned data by renaming columns, standardizing date formats, and handling missing values.

#### Key Steps:
```r
# Install necessary libraries
install.packages("tidyverse")
library(tidyverse)
library(lubridate)

# Load datasets
daily_activity <- read_csv("dailyActivity_all.csv")
daily_calories <- read_csv("daily_calories_aggr.csv")
daily_sleep <- read_csv("daily_total_sleep_aggr.csv")
daily_steps <- read_csv("distinct_daily_steps.csv")

# Clean column names
daily_calories <- daily_calories %>% rename(Id = id, TotalCalories = total_calories)
daily_sleep <- daily_sleep %>% rename(Id = id, TotalSleep = total_sleep)

# Standardize date formats
daily_activity$ActivityDate <- mdy(daily_activity$ActivityDate)

---

## 3. Process
### Data Cleaning:
- Checked for duplicates and missing values.
- Merged datasets by user ID and activity date.
- Aggregated daily metrics for analysis:
  - Total steps
  - Total calories burned
  - Sleep duration

### Key Queries:

#### Duplicate Check:
```r
duplicates <- daily_activity %>%
  group_by(Id, ActivityDate) %>%
  filter(n() > 1)

#### Missing Values Handling:
```r
daily_activity <- daily_activity %>%
  mutate(TotalSleep = ifelse(Daily_sleep == "#N/A", 0, Daily_sleep))

---

## 4. Analyze
### Summary Statistics:
Calculated key metrics like minimum, maximum, and average values for daily steps, calories burned, and sleep duration.

#### Summary Statistics in R:
```r
summary_data <- daily_activity_cleaned %>%
  summarise(
    min_steps = min(DailySteps, na.rm = TRUE),
    max_steps = max(DailySteps, na.rm = TRUE),
    avg_steps = mean(DailySteps, na.rm = TRUE),
    min_calories = min(Calories, na.rm = TRUE),
    max_calories = max(Calories, na.rm = TRUE),
    avg_calories = mean(Calories, na.rm = TRUE),
    min_sleep = min(DailySleep, na.rm = TRUE),
    max_sleep = max(DailySleep, na.rm = TRUE),
    avg_sleep = mean(DailySleep, na.rm = TRUE)
  )

### Key Insights:
- **Daily Calories Burned**: Most users burned between 1,500 and 2,500 calories daily.
- **Daily Steps**: Users generally took between 5,000 and 10,000 steps per day, with decreased activity on weekends.
- **Sleep Duration**: Most users averaged 6–8 hours of sleep per night.
- **Correlation Between Steps and Calories**: Moderate positive correlation (0.24), indicating other factors influence calorie expenditure.

---

## 5. Share

### Dashboards:
1. **Daily Activity Patterns and Wellness Metrics**:
   - Distributions of daily calories burned, steps taken, sleep duration, and activity levels.
   - Correlation between steps and calories burned.

2. **Weekly Trends in Activity, Calories, and Sleep**:
   - Visualizes weekly trends for steps, calories, and sleep duration.
   - Highlights daily fluctuations and patterns.

### Visualization Tools:
- **R (ggplot2)**: Used to create bar plots, line charts, and distributions.
- **Tableau**: Used for creating interactive dashboards.

---

## 6. Act

### Recommendations for Bellabeat:
1. **Introduce Activity Challenges and Reminders on Weekends**:
   - Encourage users to increase activity during weekends when sedentary behavior is higher.

2. **Promote Notifications for Low Activity or Calorie Burn Days**:
   - Personalized messages to encourage users to stay active and meet health goals.

### Next Steps:
- **User Segmentation Analysis**: Identify distinct user groups based on activity, calorie burn, and sleep patterns to provide personalized recommendations.
- **Enhanced Sleep Insights**: Explore relationships between sleep patterns and activity levels to improve sleep quality recommendations.

---

## Tools and Skills Demonstrated:
- **R Programming**: Data cleaning, aggregation, and statistical analysis.
- **ggplot2**: Visualization of trends and distributions.
- **Data Cleaning**: Removed duplicates, handled missing values, and standardized formats.
- **Data Analysis**: Conducted EDA to uncover patterns and correlations.
- **Data Visualization**: Created engaging plots to communicate findings effectively.

---

## Conclusion
This analysis highlights Bellabeat’s potential to enhance user engagement through data-driven insights. By identifying trends in user activity, sleep, and calorie expenditure, Bellabeat can introduce personalized features that align with users’ wellness goals.


