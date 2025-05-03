# Amazon Sales Analysis Dasboard

### Dashboard Link : https://app.powerbi.com/groups/me/reports/b99903ec-454e-41d5-9d4e-429e571fb152/11356f0f2de0e00788dc?experience=power-bi

## Problem Statement
Amazon, being one of the largest e-commerce platforms, generates a massive amount of sales data across various product categories. However, without a structured analysis, it becomes difficult for business stakeholders to monitor performance, identify growth opportunities, and understand customer preferences.

This project aims to address the need for a comprehensive sales analysis dashboard that provides actionable insights using Power BI. The focus is on:

- Tracking Year-To-Date (YTD) and Quarter-To-Date (QTD) sales trends.

- Monitoring the volume of products sold and customer reviews to gauge satisfaction.

- Visualizing performance metrics across time periods and product categories.

- Identifying the top-performing products by both sales and reviews.

### Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset is a csv file.
- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
- Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on the entire dataset".
- Step 4 : It was observed that in none of the columns errors & empty values were present.
- Step 5 : Created a Date Table to support time intelligence functions useing DAX:

      DateTable = CALENDAR(MIN(Sales[Order Date]), MAX(Sales[Order Date]))
- Step 6: Added five new columns using DAX for improved time-based analysis and visualization:
  
   1. Month Name – Extracts the abbreviated month name (e.g., Jan, Feb) to make the line chart more intuitive and user-friendly.
   2. Month Number – Captures the numerical value of the month (1–12), used to correctly sort the month names chronologically.
   3. Week – Represents the week number of the year to enable week-wise sales analysis.
   4. Quarter – Identifies the quarter (Q1–Q4) to support quarter-level sales insights.
   5. QTR – Provides a simplified label (e.g., Q1, Q2) for use in slicers, enhancing visual clarity and interactivity.

 DAX:

       Month Name = FORMAT('Date Table'[Date],"MMM")
       Month Number = MONTH('Date Table'[Date])
       Week = WEEKNUM('Date Table'[Date])
       Quarter Number = QUARTER('Date Table'[Date])
       Qtr = CONCATENATE("Qtr",'Date Table'[Quarter Number])

- Step 7 : In the report view, under the view tab, theme was selected.
- Step 8 : As per the problem statement, KPI visuals like YTD Sales, QTD Sales, YTD Products Sold, and YTD Reviews were created using DAX to provide quick insights into performance and customer engagement.

 1. YTD Sales – $2.18M
    - Displays total sales revenue generated year-to-date.
    - Indicates overall business performance for the year.

To support this KPI, a DAX measure was created for YTD Sales, which calculates the cumulative number of products sold from the beginning of the year up to the selected date, enabling year-to-date performance tracking and trend analysis...... DAX:

       YTD Sales = TOTALYTD(SUM(Amazon_Data[Price(Dollar)]),'Date Table'[Date])
       
Snap of YTD Sales KPI.

![Image](https://github.com/user-attachments/assets/4d499581-46ad-499b-95c0-b7119011646a)

2. QTD Sales – $811.09K
   - Shows total sales in the current quarter.
   - Useful for understanding quarterly growth and performance.

To support this KPI, a DAX measure was created for QTD Sales, which calculates the cumulative sales revenue from the start of the current quarter up to the selected date, allowing for precise tracking of quarterly performance and sales trends...... DAX:

      QTD Sales = TOTALQTD(SUM(Amazon_Data[Price(Dollar)]),'Date Table'[Date])
      
Snap of QTD Sales KPI.

![Image](https://github.com/user-attachments/assets/6f25f309-7963-4c66-b0a3-2f446f7e1229)

3. YTD Products Sold – 27.75k
   - Number of products sold year-to-date.
   - Tracks volume of sales and product movement.
  
To support this KPI, a DAX measure was created for YTD Products Sold, which calculates the cumulative number of products sold from the beginning of the year up to the selected date, enabling year-to-date performance tracking and trend analysis.....DAX:

      YTD Products Sold = TOTALYTD(COUNT(Amazon_Data[Product Category]),'Date Table'[Date])

Snap of YTD Products Sold KPI.

![Image](https://github.com/user-attachments/assets/16297a96-b74f-48cb-89ba-1c009627ce41)

4. YTD Reviews – 19.42M
   - Represents the number of product reviews received year-to-date.
   - Helps assess customer feedback and satisfaction trends.
  
To support this KPI, a DAX measure was created for YTD Reviews, which calculates the cumulative number of customer reviews from the beginning of the year up to the selected date, enabling continuous monitoring of customer feedback and satisfaction over time....DAX:

       YTD Reviews = TOTALYTD(SUM(Amazon_Data[Number of  reviews]),'Date Table'[Date])

Snap of YTD Reviews KPI.

![Image](https://github.com/user-attachments/assets/36f6555b-d5f1-4c5d-89a9-ebeb1ff31c51)

- Step 9: Created a line chart to visualize monthly sales trends, enabling pattern analysis and data-driven decisions by identifying high and low-performing months. The chart reveals that in the U.S., Amazon recorded its highest sales during the festive season, highlighting the significant impact of holidays on consumer purchasing behavior.

Snap of Sales By Month (Line Chart)

![Image](https://github.com/user-attachments/assets/71f9c7eb-634a-4ffe-801f-e7853020114c)
  
- Step 10: Developed a bar chart to display weekly sales distribution, allowing for granular analysis of sales performance and the identification of peak and low-activity weeks.

Snap of Sales By Week (Stacked Bar Chart)

![Image](https://github.com/user-attachments/assets/53f2ba48-cfbb-46ff-8457-412270dba71b)

- Step 11: Designed a table to showcase sales by product category, enabling a clear comparison of revenue contribution across categories for both YTD and QTD. Applied gradient formatting to visually highlight performance differences, making it easier to identify top and underperforming categories at a glance.

Snap of Sales By Product Category (Matrix)

![Image](https://github.com/user-attachments/assets/9c31e45f-f1c8-4dc4-b986-3e56c415c309)

- Step 12: Created a bar chart highlighting the top 5 products by YTD sales, helping stakeholders quickly identify best-selling items and focus marketing or inventory efforts.
        
Snap of Top 5 Products by YTD Sales (Bar Chart)    

![Image](https://github.com/user-attachments/assets/88dc6b24-057a-433c-9de6-8548c6992681)

- Step 13: Built a bar chart showing the top 5 products by YTD reviews, offering insights into customer engagement and the popularity of individual products.

Snap of Top 5 Review by YTD Review (Bar Chart) 

![image](https://github.com/user-attachments/assets/7c2a770e-6ce8-4794-bf04-ac384bc3d261)

- Step 14: Added slicers for product category and quarter to enhance interactivity, allowing users to filter and analyze the dashboard dynamically based on their focus area.

# Snapshot of Dashboard (Power BI Service)

![image](https://github.com/user-attachments/assets/3617a075-3905-4c29-b62c-2442640924c2)

 # Insights

A single page report was created on Power BI Desktop & it was then published to Power BI Service.

Following inferences can be drawn from the dashboard:

📈 Key Metrics

- YTD Sales: $2.18M

- QTD Sales: $811.09K

- Products Sold: 27.75K

- YTD Reviews: 19.42M

📅 Sales Trends

- Best Month: December

- Worst Month: February

- Sales rise significantly during the festive season (Q4).

- Weekly sales spike between weeks 39–52.

🛍️ Category Performance

- Top Category: Camera ($4.92M, 22.62%)

- Lowest: Toys ($110.8K, 5.09%)

- Gradient formatting used for visual clarity.

🔝 Top Products

- By Sales: Nikon Wi... ($34K)

- By Reviews: SanDisk 1... (0.40M)

- Electronics lead in both revenue and engagement.




    


 





  
 
 
 

       
      
