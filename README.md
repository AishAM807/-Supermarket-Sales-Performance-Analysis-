# Supermarket Sales Performance Analysis 

### Dashboard Link :

### Data Source : kaggle

## Problem Statement : 
  The supermarket generates a large amount of daily transactional data, but it is not being properly analyzed to support business decisions. Management is unable to clearly understand which branches and product categories are performing well and which require improvement. They also lack visibility into customer purchasing behavior, peak shopping hours, and preferred payment methods. This dashboard helps the supermarket management understand their sales performance and customer patterns better. Through various KPIs, product category analysis, and sales trends, they can identify high-performing and low-performing areas. It also shows peak sales periods and customer satisfaction indicators, allowing the business to improve inventory planning, staffing, and marketing strategies. By identifying these patterns, the supermarket can reduce losses, increase revenue, and make data-driven decisions to improve overall business performance.

### Steps followed :

- Step 1 : Load data into Power BI Desktop, the dataset is a csv file.
- Step 2 : Open Power Query editor & in the View tab under the Data preview section, check "column distribution", "column quality" & "column profile" options.
- Step 3 : Also since by default, the profile will be opened only for 1000 rows, you need to select "column profiling based on entire dataset".
- Step 4 : It was observed that in none of the columns errors & empty values were present, except in the column "Customer Id". Changed the data type of column named "Sales", 	   "Order Date", "Ship Date"
- Step 5 : Developed a custom Date Table using DAX and enriched it with calculated columns (e.g., Year, Month, Quarter) to enable time-intelligence reporting and trend 	   analysis.
- Step 6 : for creating "Date Table" following DAX expression was written;

			Date Table = CALENDAR(MIN('Sales Data'[Order Date]), MAX('Sales Data'[Order Date]))

- Step 7 : Created a dedicated Measures Table to organize and manage all DAX measures efficiently.
- Step 8 : Established relationships between the Sales table and the Date table in Model View.
- Step 9 : Created "Delivery Day" column to analyze shipping performance and understand how delivery time affects customer. 
- Step 10 : Used a Custom Column in Power Query to create a Delivery Day column.
- Step 11 : Implemented a dynamic YTD Sales DAX measure to track cumulative revenue performance over time and support trend analysis.
- Step 12 : for creating "Date Table" following DAX expression was written;
		
			YTD_Sales = CALCULATE(TOTALYTD([Total_Sales], 'Date Table'[Date].[Date]))

- Step 13 : Designed three report views—Sales Analysis, Product Performance, and Regional Analysis—to present different aspects of business performance.
- Step 14 : In the Regional Analysis report, visualized YTD Sales across months and years using a line chart, and implemented slicers to enable year-wise filtering.
- Step 15 : Since the sales dataset lacked a Cost column, I generated it using a calculated column in Power BI, assuming a 70% markup on sales.
	
			Cost = 'Sales Data'[Sales] * 0.70

- Step 16 : Calculated a Profit column in Power BI by subtracting Cost from Sales to analyze product and branch profitability.

			Profit = 'Sales Data'[Sales] - 'Sales Data'[Cost]


- Step 17 : Developed DAX measures for Total Sales, Total Profit, and Total Orders to enable aggregated performance analysis across the dataset.
- Step 18 : Following DAX expressions were written for the same, 
		
			Total_Sales = SUM('Sales Data'[Sales])

			Total_Profit = SUM('Sales Data'[Profit])

			Total_Orders = DISTINCTCOUNT('Sales Data'[Order ID])

- Step 19 : Created bar charts on the Sales Analysis dashboard to represent Total Sales and Total Profit by category, enabling easy identification of high-performing and low-performing product categories.
- Step 20 : Visualized Total Sales by customer segment using a donut chart and tracked monthly sales trends with an area chart for clear temporal analysis.
- Step 21 : Developed a DAX measure to highlight products generating losses, helping identify underperforming items.
	
			CALCULATE([Total_Profit], 'Sales Data'[Profit] < 5)

- Step 22 : Visualized loss-making products using a bar chart and employed the Top N filter to highlight the 10 most underperforming products.
- Step 23 : On the Product Performance page, used bar charts to visualize Total Profit by sub-category and customer segment for detailed insights.
- Step 24 : Implemented a KPI to highlight the total customer count across different segments for quick performance monitoring.
- Step 25 : Used a table to display Total Sales for the top 10 products.
- Step 27 : Created a table chart to highlight products with low profitability for focused analysis.
- Step 28 : Implemented a DAX measure to evaluate previous year sales, enabling year-over-year performance analysis and trend insights.
- Step 29 : Following DAX expression was written for the same.
  
 
			      Previous_year_sales = CALCULATE([Total_Sales], SAMEPERIODLASTYEAR('Date Table'[Date].[Date]))
       

- Step 30 : Implemented a card visual to show previous year sales and added a slicer for dynamic year-based filtering.

			
- Step 31 : Developed a DAX measure to calculate Profit Margin, enabling evaluation of product and business profitability.

			       Profit_margin % = DIVIDE([Total_Profit], [Total_Sales], 0)

- Step 32 : Implemented a card visual to show Profit_margin %


- Step 33 : In the Regional Analysis report, visualized Total Orders by region using a donut chart for clear regional comparison.
- Step 34 : Added Year and Region slicers to the dashboard, allowing interactive filtering for precise analysis of temporal and regional performance.
- Step 35 : Visualized YTD Sales by month using a combined line and stacked column chart to show trends and monthly contributions.
- Step 36 : Created a column chart to represent Delivery Days by region and segment,

 # Report Snapshot (Power BI DESKTOP)

# Insights:

Following inferences can be drawn from the dashboard;

### [1] Profit by Category:

Technology is the most profitable category (30K), followed closely by Furniture (29K) and Office Supplies (25K).

This indicates that Technology and Furniture products are driving overall profitability, while Office Supplies contribute less.

Sales by Category:

Sales values are similar to profit trends: Technology and Furniture lead (~0.10M each), with Office Supplies slightly lower (~0.08M).

Profit margins might be similar across categories, but Technology slightly edges out in terms of profit per sales.

### [2] Sales by Segment (Donut Chart) :

Consumer segment dominates total sales with 46.51%, followed by Corporate (33.42%) and Home Office (20.07%).

Consumer sales are nearly half of the total, highlighting a strong retail customer base.

Total Sales by Month (Area Chart):

Highest sales occurred early in the year (February–March), gradually declining from April onwards.

December shows the lowest sales, indicating seasonal fluctuations and a potential need for promotions in slow months.

### [3] Loss-Making Products (Bar Chart) :

Staples, Staple Envelopes, and Easy-Staple Paper are the top loss-making products.

These items may have high costs, low selling price, or low demand, requiring inventory review, pricing adjustments, or discontinuation decisions.


### [4] Total Orders by Region (Donut Chart) :

The West region contributes the highest number of orders (416 orders – 31.23%).

The East region is the second-largest contributor (365 orders – 27.4%).

The Central region (325 orders – 24.4%) and South region (226 orders – 16.97%) generate comparatively fewer orders.

This suggests the West region is the primary demand driver for the business.

### [4] KPI (Profit Margin %) :
A 30% margin suggests the business is operating at a healthy profitability level, with pricing strategies and cost control performing effectively.


