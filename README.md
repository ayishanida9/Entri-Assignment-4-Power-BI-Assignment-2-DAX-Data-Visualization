# Entri-Assignment-Power-BI-Assignment-2-DAX-Data-Visualization
# Step 1: Import the 3 CSV files
•List of Orders.csv
•Order Details.csv
•Sales target.csv
Open Power BI Desktop → Home → Get data → Text/CSV. Import all three files and click Transform data if you need to check the columns.
# Step 2: Complete data modeling first
Go to Model view (the relationship diagram icon on the left).
Your tables should connect like this:
          List of Orders
Order ID · Order Date · Customer · City · State
   Order ID · One-to-many relationship
          Order Details
Order ID · Amount · Profit · Quantity · Category · Sub-Category
          Sales target

# Instructions:-
# Calculated Columns:

Create a Calculated Column for 
* 'Category Type': Add a calculated column in the
Order Details table that combines the 'Category' and 'Sub-Category' columns into a single 'Category Type' column.
* Calculate Revenue per Order in Order Details Table: Create a calculated column in the Order Details table to compute the revenue (Amount * Quantity) per order.
* Create a Calculated Column to Categorize Sales: Add a calculated column named ‘Sales Category’ in the Order Details table that categorizes each order as 'Above Average' or 'Below Average' based on the Amount value.

# Answers
# Step 3: Create the calculated columns
Click Data view → Order Details table → New column. Enter each formula separately in the formula bar.
1. Category Type DAX
   Category Type =
'Order Details'[Category]
    & " - "
    & 'Order Details'[Sub-Category]

2. Revenue per Order
   DAX
   Revenue per Order =
'Order Details'[Amount]
    * 'Order Details'[Quantity]
  
3.Sales Category 
  DAX
  Sales Category =
   IF( 'Order Details'[Amount]
        > AVERAGE('Order Details'[Amount]),
    "Above Average",
    "Below Average")


# Calculated Measures:

* Calculate Order Count: Define a measure to count the total number of orders in the
Order Details table.
* Calculate Average Profit in Delhi: Create a measure to calculate the average profit for orders placed in Delhi.
* Calculate Year-to-Date (YTD) Sales: Define a measure to calculate the total sales amount accumulated from the earliest order date up to each order date.

# Answers:
# Step 4: Create the calculated measures
Click Order Details → New measure for each formula below.
1. Order Count
   DAX
   Order Count =
   DISTINCTCOUNT('Order Details'[Order ID])
2. Average Profit in Delhi
   DAX
   Average Profit Delhi =
  CALCULATE( AVERAGE('Order Details'[Profit]),
    'List of Orders'[City] = "Delhi")
3. Year-to-Date Sales

First, create a proper date table if you haven't already. Go to Modeling → New table and enter:
* Date Table =CALENDAR( MIN('List of Orders'[Order Date]),MAX('List of Orders'[Order Date]))
Then create a relationship between Date Table[Date] and List of Orders[Order Date]. Mark the Date Table as a date table using Table tools → Mark as date table.
* Create these measures:
Total Sales =
SUM('Order Details'[Amount])
YTD Sales =CALCULATE(  [Total Sales],
    DATESYTD('Date Table'[Date]))
    
The YTD measure accumulates sales from the beginning of each year through the date being evaluated. If the assignment intends Amount × Quantity as sales, use Revenue per Order in the measure instead.

# Data Visualization:
* Sales Target Achievement by Category: Compare actual sales with sales targets by
category using a clustered column chart.
* Max Profit Margin by Sub-Category: Analyze the maximum profit margin for each
sub-category of products using a donut chart.
* Monthly Sales Trend: Show the trend of monthly sales over time using a line chart.
* Comparison of Profit and Quantity by Sub-Category: Compare the relationship between profit and quantity sold for different sub-categories using a scatter chart.
* Comparison of Total Sales Amount and Target: Create cards to succinctly display the total sales amount alongside the sales target for quick comparison and analysis. Also, create a multi-row card to display the minimum target for each segment.
* Sales Performance Matrix: Build a matrix view to analyze how actual sales compare to sales targets across different categories and months.
* Geographic Sales Analysis: Visualize total sales on a map by city to identify regional sales patterns.
* Sales Distribution by Sub-Category: Represent the sales distribution across different sub-categories using a treemap.
Order Count Analysis by State:
* Create a funnel chart to visualize the distribution of order counts across different states.

# Answers:
# Step 5: Create the visualizations
Go to Report view. Select the chart type from the Visualizations pane and drag the listed fields into the appropriate wells.

1. Sales Target Achievement by Category
Clustered column chart
•X-axis: Category
•Y-axis: Total Sales and Target
•Legend: automatically uses the two measures as separate series
Compare actual sales with target for each category. Ensure the target is summarized correctly.

2. Max Profit Margin by Sub-Category
  Donut Chart
•Legend: Sub-Category
•Values: Profit Margin → Maximum

3. Monthly Sales Trend
   Line Chart
•X-axis: Order Date or a proper Year-Month field
•Y-axis: Total Sales
Sort dates chronologically, not alphabetically by month name.

4. Profit vs Quantity by Sub-Category
   Scatter chart
•X-axis: Quantity
•Y-axis: Profit
•Details: Sub-Category
Use summed Quantity and summed Profit for each sub-category to compare them.

5. Total Sales, Target and Minimum Target
Cards + multi-row card/Table
Create two measures:
Total Target =
SUM('Sales target'[Target])

Minimum Target =
MIN('Sales target'[Target])

•Card 1: Total Sales
•Card 2: Total Target
•Multi-row card: Segment and Minimum Target
If your target table has no Segment column, use the actual field available or check the assignment's intended target breakdown.

Table visual use 
1. Select Table Visual
2. Add Fields
Category
Minimum Target

6. Sales Performance Matrix
   Matrix
•Rows: Category
•Columns: Year-Month
•Values: Total Sales and Total Target
This helps you identify months and categories where sales are above or below target.

7. Geographic Sales Analysis
   Map
•Location: City
•Bubble size: Total Sales
Set the City column's data category to City under Column tools if needed.

8. Sales Distribution by Sub-Category
   Treemap
•Category: Sub-Category
•Values: Total Sales
Larger rectangles represent sub-categories with higher sales.

9. Order Count by State
    Funnel chart
•Category: State
•Values: Order Count
Sort by Order Count in descending order to make the state-wise comparison easier to read.






