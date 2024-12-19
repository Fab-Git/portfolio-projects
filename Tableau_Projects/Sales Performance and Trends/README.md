# Sales Performance and Trends (Dashboard)

## Project Overview
This project analyzes **sales data from an online retail store** to provide actionable insights into product demand, customer segmentation, and regional revenue trends. The primary goal is to assist the company in optimizing its sales strategy by identifying high-demand regions, high-value customers, and seasonal trends.

---

## Data Analysis Steps

### **Data Cleaning**
1. **Removed negative quantities**:
   - Excluded transactions with negative product quantities (e.g., returns or data entry errors) for accurate demand analysis.
2. **Filtered out negative prices**:
   - Eliminated transactions with negative unit prices to avoid skewed revenue calculations.

### **Data Preparation**
1. **Formatted dates**:
   - Cleaned and formatted the `InvoiceDate` field to enable time-series analysis.
2. **Calculated revenue**:
   - Created a calculated field for total revenue: `Quantity * Unit Price`.
3. **Filtered countries**:
   - Excluded the United Kingdom for expansion-focused analyses, emphasizing other countries.

---

## Key Insights & Visualizations

### 1. **Global Product Demand**
- **Visualization**: Tree Map of product demand by country.
- **Insight**:
  - The Netherlands, EIRE, and Germany exhibited the highest product demand, signaling strong market potential.

### 2. **Monthly Revenue Trends (2011)**
- **Visualization**: Line chart of monthly revenue.
- **Insight**:
  - Revenue peaked in **November**, likely due to holiday shopping or promotional events.

### 3. **Top 10 Countries by Revenue**
- **Visualization**: Bar chart ranking countries by revenue.
- **Insight**:
  - The Netherlands and EIRE were the top revenue-generating countries.

### 4. **Bottom 10 Countries by Revenue**
- **Visualization**: Bar chart showing countries with the lowest revenue.
- **Insight**:
  - Saudi Arabia, Bahrain, and the Czech Republic generated the least revenue, highlighting underperforming regions.

### 5. **Top 10 Customers by Revenue**
- **Visualization**: Bar chart of high-value customers.
- **Insight**:
  - The top customer generated over **$280,000**, emphasizing the importance of retention strategies for high-value clients.

---

## Insights from the Dashboard

1. **Seasonal Sales Trends**:
   - Revenue spikes in **November and December** indicate strong seasonal demand driven by holidays and promotions.
2. **Top-Performing Regions**:
   - The Netherlands, EIRE, and Germany lead in revenue, showing consistent demand across product categories.
3. **Customer Concentration**:
   - A small percentage of high-value customers contribute significantly to overall revenue.
4. **Underperforming Regions**:
   - Countries such as Saudi Arabia and Brazil have low revenue, highlighting potential market challenges.

---

## Recommendations

1. **Enhance Marketing Around Seasonal Peaks**:
   - Invest in seasonal promotions during **November** and **December** to capitalize on high-demand periods.
2. **Implement Customer Retention Strategies**:
   - Develop loyalty programs targeting the **top 10 revenue-generating customers**, offering personalized discounts and exclusive perks.
3. **Boost Sales During Off-Peak Seasons**:
   - Launch targeted campaigns and promotions (e.g., flash sales) during slower months like **February** and **March**.
4. **Expand in High-Demand Regions**:
   - Introduce new product lines in countries like EIRE and Germany, focusing on local preferences and faster shipping times.

---

## Tools and Technologies Used
- **Excel**: Data cleaning and preparation.
- **Tableau**: Data visualization and dashboard creation.

---

