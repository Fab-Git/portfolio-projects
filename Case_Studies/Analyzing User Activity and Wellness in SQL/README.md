# Bellabeat Wellness Device Case Study: Analyzing User Activity and Wellness Patterns

## Introduction
The **Bellabeat Wellness Device Case Study** explores user activity patterns, sleep behavior, and calorie expenditure to gain insights into wellness trends. This analysis aims to help **Bellabeat**, a wellness technology company, understand user behavior and enhance product engagement and impact on health. 

By leveraging data from Bellabeat devices, the study identifies actionable insights to inform product design and marketing strategies. The analysis follows a structured 6-step framework: **Ask, Prepare, Process, Analyze, Share, and Act**, each documented in detail.

---

## Framework
1. **Ask**: Define the business task and set objectives.
2. **Prepare**: Gather and clean data for analysis.
3. **Process**: Conduct exploratory data analysis (EDA) and calculate summary statistics.
4. **Analyze**: Identify patterns, correlations, and outliers.
5. **Share**: Visualize insights using dashboards.
6. **Act**: Make data-driven recommendations.

---

## 1. Ask
### Objective:
- Analyze activity and wellness data to understand user behavior and trends.
- Identify actionable insights for product improvements and marketing strategies.

### Business Questions:
- What are the daily activity patterns of Bellabeat users?
- How do steps, calories, and sleep patterns vary across the week?
- Are there any correlations between steps taken and calories burned?

---

## 2. Prepare
### Data Sources:
- **Bellabeat Wellness Data**: Metrics such as daily steps, calories burned, activity levels, and sleep duration.

### Data Cleaning:
- Merged and cleaned data to remove duplicates and ensure consistency.
- Handled missing values and verified data types for accuracy.

#### SQL Queries:
**Count of Records and Unique Users**
```sql
# Total records
SELECT COUNT(*) as total_records FROM `Bellabeat_wellness.daily_activity_all`;

# Unique users
SELECT COUNT(DISTINCT id) as unique_users FROM `Bellabeat_wellness.daily_activity_all`;

# Handling Missing Values in Daily Sleep
UPDATE `Bellabeat_wellness.daily_activity_all`
SET Daily_sleep = 0
WHERE Daily_sleep = '#N/A';
```
---

## 3. Process
### Exploratory Data Analysis (EDA):
- Performed initial data exploration using SQL.
- Calculated basic statistics such as min, max, and average values for daily steps, calories, and sleep.

**SQL Query:**
**Basic Statistics**
```sql
WITH distinct_steps AS (
  SELECT DISTINCT id, ActivityDate, ID_ActivityDate, DailySteps
  FROM `Bellabeat_wellness.daily_activity_all`
),
aggr_calories AS (
  SELECT id, ActivityDate, SUM(Calories) AS total_calories
  FROM `Bellabeat_wellness.daily_activity_all`
  GROUP BY id, ActivityDate
),
aggr_sleep AS (
  SELECT id, ActivityDate, SUM(CAST(Daily_sleep AS FLOAT64)) AS total_sleep
  FROM `Bellabeat_wellness.daily_activity_all`
  WHERE Daily_sleep IS NOT NULL AND Daily_sleep <> ''
  GROUP BY id, ActivityDate
)
SELECT
  MIN(DailySteps) as min_steps,
  MAX(DailySteps) as max_steps,
  ROUND(AVG(DailySteps), 2) as avg_steps,
  MIN(ac.total_calories) as min_calories,
  MAX(ac.total_calories) as max_calories,
  ROUND(AVG(ac.total_calories), 2) as avg_calories,
  MIN(asl.total_sleep) as min_sleep,
  MAX(asl.total_sleep) as max_sleep,
  ROUND(AVG(asl.total_sleep), 2) as avg_sleep
FROM distinct_steps ds
INNER JOIN aggr_calories ac ON ds.id = ac.id
INNER JOIN aggr_sleep asl ON asl.id = ds.id;
```
---

## 4. Analyze
### Key Insights:
- **Daily Calories Burned:** Most users burned between 1,500 and 2,500 calories daily.
- **Daily Steps:** Users generally took between 5,000 and 10,000 steps per day, with a decrease on weekends.
- **Activity Levels Across the Week:** Sedentary minutes were significantly high during weekends.
- **Correlation Between Steps and Calories:** Weak positive correlation (0.24), suggesting other factors impact calorie burn.
- **Sleep Duration:** Users averaged 6–8 hours of sleep per night.

**SQL Query:**
**Correlation Between Steps and Calories**
```sql
WITH distinct_steps AS (
  SELECT DISTINCT id, ActivityDate, ID_ActivityDate, DailySteps
  FROM `Bellabeat_wellness.daily_activity_all`
),
aggr_calories AS (
  SELECT id, ActivityDate, SUM(Calories) AS total_calories
  FROM `Bellabeat_wellness.daily_activity_all`
  GROUP BY id, ActivityDate
)
SELECT CORR(DailySteps, total_calories) AS correlation_steps_calories
FROM distinct_steps ds
INNER JOIN aggr_calories ac ON ac.id = ds.id;

**Result:** Correlation between steps and calories = **0.24**.
```
---

## 5. Share

### Dashboards:
1. **Daily Activity Patterns and Wellness Metrics**:
   - Includes distributions of daily calories burned, steps taken, sleep duration, and activity levels.
   - Shows the correlation between steps and calories burned.

2. **Weekly Trends in Activity, Calories, and Sleep**:
   - Visualizes weekly trends for steps, calories, and sleep duration.
   - Highlights daily fluctuations and patterns.

---

## 6. Act

### Recommendations for Bellabeat:
1. **Introduce Activity Challenges and Reminders on Weekends**:
   - Encourage users to increase activity during weekends when sedentary time is higher.

2. **Promote Notifications for Low Activity or Calorie Burn Days**:
   - Personalized messages to encourage users to stay active and meet health goals.

### Next Steps:
- **User Segmentation Analysis**: Identify distinct user groups based on activity and sleep patterns for personalized recommendations.
- **Enhanced Sleep Insights**: Explore the relationship between sleep patterns and activity levels to improve sleep quality recommendations.

---

## Tools and Skills Demonstrated:
- **SQL**: Data cleaning, aggregation, and summary statistics.
- **Spreadsheet**: Data preparation and preprocessing.
- **Tableau**: Visualization and dashboard creation.
- **Data Cleaning**: Ensured consistency and accuracy by handling missing values.
- **Data Analysis**: Conducted exploratory analysis to uncover patterns and insights.
- **Data Visualization**: Created engaging visuals to support findings and recommendations.

---

## Conclusion
This analysis highlights Bellabeat’s potential to enhance user engagement through personalized features and data-driven insights. By identifying trends in user activity, sleep, and calorie expenditure, Bellabeat can introduce tailored solutions to align with users’ wellness goals.

