# Exploring Nutritional Patterns & Health Insights with Data Analysis

## Overview
This project explores daily food consumption patterns using a dataset of 10,000 food entries, analyzing their nutritional content. I conducted data cleaning, exploratory data analysis (EDA), and visualization to uncover trends in macronutrient intake, high-calorie foods, and unhealthy dietary habits.

Through Python (**Pandas**, **Matplotlib**, **Seaborn**), I extracted valuable insights into caloric discrepancies, macronutrient distribution, and high-risk food items, enabling better dietary awareness.

---

## Key Objectives
- **Macronutrient Breakdown:** How protein, carbohydrates, and fats vary across different food categories and meal types.
- **Food Category Insights:** Identifying the food groups contributing the most to daily calorie intake.
- **High-Risk Foods:** Finding foods with excessive sodium, cholesterol, and sugar levels.
- **Trend Analysis Over Time:** Investigating how calorie and nutrient intake fluctuates monthly.
- **Comparison of Provided vs. Calculated Calories:** Assessing data accuracy in reported nutritional values.

---

## Data Cleaning & Preprocessing
- Removed duplicates and missing values.
- Converted dates into datetime format for trend analysis.

---

## Key Findings & Visualizations

### 1. Macronutrient Breakdown
```python
meal_macronutrient_ratios = df.groupby("Meal_Type")[["Protein (g)","Carbohydrates (g)","Fat (g)"]].mean()
meal_macronutrient_ratios["Protein %"] = meal_macronutrient_ratios["Protein (g)"] * 4 / (meal_macronutrient_ratios["Protein (g)"] * 4 + meal_macronutrient_ratios["Carbohydrates (g)"] * 4 + meal_macronutrient_ratios["Fat (g)"] * 9) * 100
meal_macronutrient_ratios["Carbohydrates %"] = meal_macronutrient_ratios["Carbohydrates (g)"] * 4 / (meal_macronutrient_ratios["Protein (g)"] * 4 + meal_macronutrient_ratios["Carbohydrates (g)"] * 4 + meal_macronutrient_ratios["Fat (g)"] * 9) * 100
meal_macronutrient_ratios["Fat %"] = meal_macronutrient_ratios["Fat (g)"] * 9 / (meal_macronutrient_ratios["Protein (g)"] * 4 + meal_macronutrient_ratios["Carbohydrates (g)"] * 4 + meal_macronutrient_ratios["Fat (g)"] * 9) * 100
meal_macronutrient_ratios = meal_macronutrient_ratios[["Protein %","Carbohydrates %","Fat %"]]
```

**Insight:** Different meal types and food categories have distinct macronutrient compositions.

---

### 2. Food Category Contributions to Calorie Intake
```python
food_category_calories = df.groupby("Category")["Calories (kcal)"].mean().sort_values(ascending = False)
```

**Insights:**
- Some categories, such as grains and dairy, contribute significantly more to daily calorie intake than vegetables or fruits.
- High sodium content is a concern across all food categories, potentially indicating a reliance on processed or salty foods.
- Cholesterol levels are relatively balanced but higher in animal-based foods, reinforcing the importance of moderation in dairy and meat consumption.

---

### 3. High-Sodium, High-Cholesterol, and High-Sugar Foods
```python
top_sodium_foods = df.sort_values(by = "Sodium (mg)", ascending= False).head(10)
top_cholesterol_foods = df.sort_values(by = "Cholesterol (mg)", ascending = False).head(10)
top_sugar_foods = df.sort_values(by="Sugars (g)", ascending=False).head(10)
```

**Insights:**
- Certain natural foods like salmon, cheese, and spinach have high sodium content, alongside some processed items like butter and chocolate.
- While dairy (cheese) and meat (pork chop) contain cholesterol, some unexpected items like tomato and coffee also appear on the list, possibly due to data inconsistencies.

---

### 4. Trend Analysis Over Time
```python
df["Year-Month"] = df["Date"].dt.to_period("M")
trend_analysis = df.groupby("Year-Month")[["Calories (kcal)", "Protein (g)", "Carbohydrates (g)", "Fat (g)"]].mean()
```

**Insights:**
- Some months have higher calorie consumption, possibly due to holidays, seasonal food availability, or lifestyle changes.
- The overall diet composition remains stable, implying no major dietary shifts in macronutrient intake.

---

### 5. Comparison of Provided vs. Calculated Calories
```python
df['Calculated_Calories'] = df['Protein (g)'] * 4 + df['Carbohydrates (g)'] * 4 + df['Fat (g)'] * 9
df['Macronutrient_Percentage'] = df['Calculated_Calories'] / df['Calories (kcal)'] * 100
```

**Insights:**
- There is a pattern of underreported calorie values, suggesting potential inaccuracies in the dataset.
- Food items with lower reported calories tend to have a much higher calculated calorie range, which could indicate missing data or incorrect food labeling.

---

## Technical Tools and Skills
- **Data Cleaning & Preprocessing**
- **Data Visualization & Storytelling**
- **Python (Pandas, Matplotlib, Seaborn)**
- **Jupyter Notebook**

---

## Next Steps
- **Further Investigate High Discrepancy Foods:** Identify specific food categories or items with the largest calorie misreporting.
- **Expand Analysis to Dietary Impact:** Investigate how these trends affect health metrics like BMI and nutritional balance.
- **Develop a Predictive Model:** Use machine learning to estimate missing nutritional values.

---

## Conclusion
This project highlights the importance of accurate nutritional data and its impact on dietary choices. The analysis uncovered significant discrepancies in reported calorie values, emphasizing the need for better data integrity in food tracking. Additionally, identifying high-risk foods and nutrient trends provides valuable insights for health-conscious decision-making.

