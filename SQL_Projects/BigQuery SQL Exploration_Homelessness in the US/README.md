# U.S. Homelessness Trends Analysis (SQL & BigQuery)

## Project Overview
This project focuses on analyzing the **Point-in-Time Homelessness Count dataset** from HUD to uncover key insights into homelessness trends across U.S. states and Continuum of Care (CoC) areas. By leveraging SQL within Google BigQuery, the project evaluates the distribution of homelessness, assesses the effectiveness of shelter programs, and identifies regions facing specific homelessness challenges.

---

## Tools & Technologies
- **SQL**: For querying and analyzing large datasets.
- **Google BigQuery**: Cloud-based data analytics platform.
- **Exploratory Data Analysis (EDA)**: To uncover trends and patterns.

---

## Objectives
1. Analyze and understand homelessness data schema and key metrics.
2. Answer questions about homelessness trends using SQL queries.
3. Identify regions with specific needs, such as unaccompanied homeless youth or high unsheltered homelessness rates.
4. Compare state homelessness rates with population data to identify disparities.

---

## Dataset Details
- **Dataset**: Point-in-Time Homelessness Count
- **Source**: HUD (U.S. Department of Housing and Urban Development)
- **Key Table**: `hud_pit_by_coc`
- **Important Columns**:
  - `CoC_Name`: Continuum of Care area.
  - `State`: U.S. state or territory.
  - `Overall_Homeless`: Total homeless population.
  - `Sheltered_Homeless` & `Unsheltered_Homeless`: Breakdown of homeless populations.
  - `Homeless_Unaccompanied_Youth_Under_18`: Count of unaccompanied homeless youth.
  - `Count_Year`: Year of the homelessness count.

---

## Key Insights & SQL Queries

### 1. **Top 3 Areas for Unaccompanied Homeless Youth Under 18 (2018)**
- **SQL Query**:
  ```sql
  SELECT CoC_Name, Homeless_Unaccompanied_Youth_Under_18
  FROM `Exploration_Project.homelessness`
  WHERE Count_Year = 2018
  ORDER BY Homeless_Unaccompanied_Youth_Under_18 DESC
  LIMIT 3;

**Insight:** Identified the top 3 CoC areas with the highest number of unaccompanied homeless youth under 18 in 2018, aiding program prioritization.

### 2. **Homelessness Trends in Delaware**
- **SQL Query**:
  ```sql
  SELECT Count_Year, Unsheltered_Homeless
  FROM `Exploration_Project.homelessness`
  WHERE State = 'DE'
  ORDER BY Count_Year;

**Insight:** Tracked unsheltered homelessness in Delaware over the past 7 years to monitor trends.

### 3. **Safe Haven Program Analysis (2018)**
- **SQL Query**:
  ```sql
  SELECT CoC_Name, Sheltered_SH_Homeless
  FROM `Exploration_Project.homelessness`
  WHERE Count_Year = 2018 AND Sheltered_SH_Homeless > 0;

**Insight:** Identified CoC areas with active Safe Haven shelters in 2018 to evaluate program presence despite funding cuts.

### 4. **Top 7 States by Homeless Population (2018)**
- **SQL Query**:
  ```sql
  SELECT State, SUM(Overall_Homeless) AS total_homeless_population
  FROM `Exploration_Project.homelessness`
  WHERE Count_Year = 2018
  GROUP BY State
  ORDER BY total_homeless_population DESC
  LIMIT 7;
**Insight:** Highlighted states with the highest homeless populations for focused resource allocation.

### 5. **Shelter Effectiveness: Locations with Low Unsheltered Homelessness**
- **SQL Query**:
  ```sql
  SELECT CoC_Name, Overall_Homeless, Unsheltered_Homeless,
        ROUND(Unsheltered_Homeless / Overall_Homeless * 100, 2) AS unsheltered_percentage
  FROM `Exploration_Project.homelessness`
  WHERE Count_Year = 2018
    AND Overall_Homeless > 1000
    AND Unsheltered_Homeless < 100
    AND ROUND(Unsheltered_Homeless / Overall_Homeless * 100, 2) < 2;

**Insight:** Found locations where fewer than 2% of the homeless population were unsheltered, showcasing effective sheltering practices.

### 6. **Overrepresentation vs. Underrepresentation**
- **Overrepresented States:** New York (NY), Washington (WA), Massachusetts (MA), and Oregon (OR) have disproportionately high homelessness relative to their population.
- **Underrepresented States:** Texas (TX), Pennsylvania (PA), Illinois (IL), and Ohio (OH) rank lower in homelessness compared to their population size.

## Challenges & Learnings

### Handling Missing Data:
- Addressed NULL values and inconsistencies to ensure reliable analysis.

### State Identification:
- Used SQL functions (e.g., `LEFT()`) to extract state names from CoC identifiers.

### Actionable Insights:
- Provided data-driven insights to guide resource allocation and policy-making.

---

## Recommendations

### Expand Shelter Programs:
- Focus on areas with high unaccompanied homeless youth and low shelter effectiveness.

### Address Overrepresented States:
- Allocate resources to states with disproportionately high homelessness rates.

### Study Shelter Effectiveness:
- Investigate best practices in locations with less than 2% unsheltered homelessness.

### Implement Safe Haven Programs:
- Support active Safe Haven locations and expand the program where needed.

---

## Future Enhancements

### Data Visualization:
- Develop dashboards in Tableau or Power BI for visualizing key trends.

### Predictive Analysis:
- Use historical data to predict future homelessness trends.

### Integrate Additional Datasets:
- Incorporate socio-economic and housing data for deeper analysis.

---

## Tools Used
- **Google BigQuery**: For data storage and querying.
- **SQL**: For data exploration and analysis.

---

## Conclusion
This project provided valuable insights into homelessness trends across the U.S., identifying regions requiring more support and highlighting effective shelter programs. By leveraging SQL and BigQuery, the analysis can inform resource allocation and policy-making to address homelessness challenges more effectively.




