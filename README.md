# Amazon Sales Analysis Dasboard

### Dashboard Link : https://app.powerbi.com/groups/me/reports/384d017e-e935-44dc-9e7d-1626c1a36de1/ReportSection

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

- Step 6 : In the report view, under the view tab, theme was selected.
- Step 7 : Since the problem statement required KPI visuals

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


YTD Products Sold – 27.75k

Number of products sold year-to-date.

Tracks volume of sales and product movement.

YTD Reviews – 19.42M

Represents the number of product reviews received year-to-date.

Helps assess customer feedback and satisfaction trends.
- Step 8 : Visual filters (Slicers) were added for four fields named "Class", "Customer Type", "Gate Location" & "Type of travel".
- Step 9 : Two card visuals were added to the canvas, one representing average departure delay in minutes & other representing average arrival delay in minutes.
           Using visual level filter from the filters pane, basic filtering was used & null values were unselected for consideration into average calculation.
           
          Although, by default, while calculating average, blank values are ignored.
- Step 10 : A bar chart was also added to the report design area representing the number of satisfied & neutral/unsatisfied customers. While creating this visual, field named "Gender" was also added to the Legends bucket, thus number of customers are also seggregated according the gender. 
- Step 11 : Ratings Visual was used to represent different ratings mentioned below,

  (a) Baggage Handling

  (b) Check-in Services
  
  (c) Cleanliness
  
  (d) Ease of online booking
  
  (e) Food & Drink
  
  (f) In-flight Entertainment

  (g) In-flight Service
  
  (h) In-flight wifi service
  
  (i) Leg Room service
  
  (j) On-board service
  
  (k) Online boarding
  
  (l) Seat comfort
  
  (m) Departure & arrival time convenience
  
In our dataset, Some parameters were assigned value 0, representing those parameters are not applicable for some customers.

All these values have been ignored while calculating average rating for each of the parameters mentioned above.

- Step 12 : In the report view, under the insert tab, two text boxes were added to the canvas, in one of them name of the airlines was mentioned & in the other one company's tagline was written.
- Step 13 : In the report view, under the insert tab, using shapes option from elements group a rectangle was inserted & similarly using image option company's logo was added to the report design area. 
- Step 14 : Calculated column was created in which, customers were grouped into various age groups.

for creating new column following DAX expression was written;
       
        Age Group = 
        
        if(airline_passenger_satisfaction[Age]<=25, "0-25 (25 included)",
        
        if(airline_passenger_satisfaction[Age]<=50, "25-50 (50 included)",
        
        if(airline_passenger_satisfaction[Age]<=75, "50-75 (75 included)",
        
        "75-100 (100 included)")))
        
Snap of new calculated column ,

![Snap 1](https://github.com/user-attachments/assets/17d4c08c-a663-4584-9b5c-4eb17e1e92ae)

        
- Step 15 : New measure was created to find total count of customers.

Following DAX expression was written for the same,
        
        Count of Customers = COUNT(airline_passenger_satisfaction[ID])
        
A card visual was used to represent count of customers.

![Snap_Count](https://user-images.githubusercontent.com/102996550/174090154-424dc1a4-3ff7-41f8-9617-17a2fb205825.jpg)

        
 - Step 16 : New measure was created to find  % of customers,
 
 Following DAX expression was written to find % of customers,
 
         % Customers = (DIVIDE(airline_passenger_satisfaction[Count of Customers], 129880)*100)
 
 A card visual was used to represent this perecntage.
 
 Snap of % of customers who preferred business class
 
 ![Snap_Percentage](https://user-images.githubusercontent.com/102996550/174090653-da02feb4-4775-4a95-affb-a211ca985d07.jpg)

 
 - Step 17 : New measure was created to calculate total distance travelled by flights & a card visual was used to represent total distance.
 
 Following DAX expression was written to find total distance,
 
         Total Distance Travelled = SUM(airline_passenger_satisfaction[Flight Distance])
    
 A card visual was used to represent this total distance.
 
 
 ![Snap_3](https://user-images.githubusercontent.com/102996550/174091618-bf770d6c-34c6-44d4-9f5e-49583a6d5f68.jpg)
 
 - Step 18 : The report was then published to Power BI Service.
 
 
![Publish_Message](https://user-images.githubusercontent.com/102996550/174094520-3a845196-97e6-4d44-8760-34a64abc3e77.jpg)

# Snapshot of Dashboard (Power BI Service)

![dashboard_snapo](https://user-images.githubusercontent.com/102996550/174096257-11f1aae5-203d-44fc-bfca-25d37faf3237.jpg)

 
 # Report Snapshot (Power BI DESKTOP)

 
![Dashboard_upload](https://user-images.githubusercontent.com/102996550/174074051-4f08287a-0568-4fdf-8ac9-6762e0d8fa94.jpg)

# Insights

A single page report was created on Power BI Desktop & it was then published to Power BI Service.

Following inferences can be drawn from the dashboard;

### [1] Total Number of Customers = 129880

   Number of satisfied Customers (Male) = 28159 (21.68 %)

   Number of satisfied Customers (Female) = 28269 (21.76 %)

   Number of neutral/unsatisfied customers (Male) = 35822 (27.58 %)

   Number of neutral/unsatisfied customers (Female) = 37630 (28.97 %)


           thus, higher number of customers are neutral/unsatisfied.
           
### [2] Average Ratings

    a) Baggage Handling - 3.63/5
    b) Check-in Service - 3.31/5
    c) Cleanliness - 3.29/5
    d) Ease of online booking - 2.88/5
    e) Food & Drink - 3.21/5
    f) In-flight Entertainment - 3.36/5
    g) In-flight service - 3.64/5
    h) In-flight Wifi service - 2.81/5
    i) Leg room service - 3.37/5
    j) On-board service - 3.38/5
    k) Online boarding - 3.33/5
    l) Seat comfort - 3.44/5
    m) Departure & arrival convenience - 3.22/5
  
  while calculating average rating, null values have been ignored as they were not relevant for some customers. 
  
  These ratings will change if different visual filters will be applied.  
  
  ### [3] Average Delay 
  
      a) Average delay in arrival(minutes) - 15.09
      b) Average delay in departure(minutes) - 14.71
Average delay will change if different visual filters will be applied.

 ### [4] Some other insights
 
 ### Class
 
 1.1) 47.87 % customers travelled by Business class.
 
 1.2) 44.89 % customers travelled by Economy class.
 
 1.3) 7.25 % customers travelled by Economy plus class.
 
         thus, maximum customers travelled by Business class.
 
 ### Age Group
 
 2.1)  21.69 % customers belong to '0-25' age group.
 
 2.2)  52.44 % customers belong to '25-50' age group.
 
 2.3)  25.57 % customers belong to '50-75' age group.
 
 2.4)  0.31 % customers belong to '75-100' age group.
 
         thus, maximum customers belong to '25-50' age group.
         
### Customer Type

3.1) 18.31 % customers have customer type 'First time'.

3.2) 81.69 % customers have customer type 'returning'.
       
       thus, more customers have customer type 'returning'.

### Type of travel

4.1) 69.06 % customers have travel type 'Business'.

4.2) 30.94 % customers have travel type 'Personal'.

        thus, more customers have travel type 'Business'.
