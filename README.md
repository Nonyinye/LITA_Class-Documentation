# Capstone_Project_Sales_Dataset

## Project Title: Sales Transaction 

* [Project Overview](ProjectOverview)

* [Column Descriptions](columndescriptions)

* [Data Source](datasource)

* [Tools Used](toolsused)

* [Data Cleaning and Preparations](datacleaningandpreparations)

* [Exploratory Data Analysis](exploratorydataanalysis)

For Sales Data

For Customer Data

Data Analysis

Data Visualization

My Result

For Sales Data

For Customer Data

### Project Overview
This dataset captures transactional sales data, providing a detailed view of customer orders, including product, region, and revenue information. It is ideal for analyzing sales trends, and regional performance, enabling insights into the drivers of revenue and high-demand products.

### Column Descriptions
* OrderID: A unique identifier for each order.
* CustomerId: A unique identifier for each customer placing an order.
* Product: The specific product purchased in each transaction.
* Region: The geographical location (e.g., North, South, East, West) where the order was placed.
* OrderDate: The date when the order was made.
* Quantity: The number of units purchased for each product in an order.
* UnitPrice: The price per unit of the product.
* Total Sales: The total sales value for the order, calculated as Quantity * UnitPrice
* Revenue: The total sales value for the order, calculated as Quantity * UnitPrice
  
### Data Source
The main data sources for this analysis is the "Dataset Sales.csv" which is an open-source datasets available for free download from online repositories like Kaggle, FRED, or other similar platforms.

### Tools Used
- Excel: Employed for data cleaning and visualization.

- SQL: Utilized for data cleaning through queries.

- Power BI: Used for both data cleaning and visualization.

### Data Cleaning and Preparations
In the intial phase of Data Cleaning and Preparations, the following actions were performed;
* Data loading and Inspection
* Handling missing variables
* Data Cleaning and Formatting

### Exploratory Data Analysis
EDA involved the exploratory of the Sales Data to answer some questions about the dataset such as;
1. Retrieve the total sales for each product category.
2. Find the number of sales transactions in each region.
3. Find the highest-selling product by total sales value.
4. Calculate total revenue per product.
5. Calculate monthly sales totals for the current year.
6. Find the top 5 customers by total purchase amount.
7. Calculate the percentage of total sales contributed by each region.
8. Identify products with no sales in the last quarter.

### Data Analysis
This is where some basic lines of code or queries or even some of the DAX expressions used during data analysis were included;
```
SELECT * FROM[dbo].[LITA Capstone Sales Data]

---Add Total Sales Coloumn---
ALTER TABLE [dbo].[LITA Capstone Sales Data]
ADD Total_Sales int
UPDATE [dbo].[LITA Capstone Sales Data]
SET Total_Sales = (Quantity*UnitPrice)

 
---Q1  Retrieve the total sales for each product category.---
SELECT Product,SUM(Total_Sales) as Total_Sales
FROM [LITA Capstone Sales Data]
GROUP BY Product

---Q2 Find the number of sales transactions in each region.--
SELECT Region,SUM(Total_Sales) as Total_Sales
FROM [LITA Capstone Sales Data]
GROUP BY Region

--- Q3 Find the highest-selling product by total sales value.
SELECT top 1Product,SUM(Total_Sales) as Total_Sales
FROM [LITA Capstone Sales Data]
GROUP BY Product
Order By Total_Sales Desc

--- Q4 Calculate total revenue per product--
SELECT Product,SUM(Quantity*UnitPrice) as Total_Revenue
FROM [LITA Capstone Sales Data]
GROUP BY Product

ALTER TABLE [dbo].[LITA Capstone Sales Data]
ADD OrderMonth nvarchar(50)

UPDATE [LITA Capstone Sales Data]
SET OrderMonth = DATENAME(MONTH, OrderDate)

ALTER TABLE [dbo].[LITA Capstone Sales Data]
ADD OrderYear int

UPDATE [dbo].[LITA Capstone Sales Data]
SET OrderYear = Year(OrderDate)

--- Rename Column---
EXEC sp_rename
'[LITA Capstone Sales Data].Total_Sales','Revenue', 'COLUMN';

SELECT * FROM [LITA Capstone Sales Data]

--Q5 Calculate monthly sales totals for the current year(2024)--

SELECT OrderMonth,SUM(Total_Sales) as Total_Sales
FROM [LITA Capstone Sales Data]
WHERE OrderYear = 2024
GROUP BY OrderMonth

--- Q6 find the top 5 customers by total purchase amount
SELECT  Top 5 Customer_Id,SUM(Total_Sales) AS Total_Purchase
FROM [LITA Capstone Sales Data]
GROUP BY Customer_Id
ORDER BY Total_Purchase DESC

---Q7 calculate the percentage of total sales contributed by each region.
SELECT Region,SUM(Revenue)/SUM(Total_Sales)*0.1 AS Percentage_of_Total_Sales
FROM [LITA Capstone Sales Data]
GROUP BY Region
ORDER BY Percentage_of_Total_Sales

--Q8 Identify products with no sales in the last quarter
SELECT Product,SUM(Total_Sales) AS Sales
FROM [LITA Capstone Sales Data]
WHERE MONTH(OrderDate) BETWEEN 10 AND 12  -- Months 10, 11, and 12 (October to December)
GROUP BY Product
HAVING SUM(Total_Sales)= 0

SELECT * FROM[dbo].[LITA Capstone Sales Data]
```

### Data Visualization


### Result for Sales Data Analysis
Our Sales Data analysis tells a story of what our customers love and how they shop. Shoes are the star of our sales, selling over 600,000 units and becoming our best-selling product. Meanwhile, socks, though popular, came in last with about 180,000 sold. Each month brought its own pattern, with February being the busiest month of all. As the year went on, the first and second quarters showed strong, high sales. But as summer turned into fall, sales began to drop, and by the fourth quarter, they were down by over 50%. Looking at different regions, the South led the way, making up 44% of our sales, followed by the East at 23%, the North at 18%, and finally, the West with 14%. Each area added its own flavor to our overall numbers, but together, they showed the store’s success across the map. One surprising insight was that higher-priced items usually sold better. Customers seemed to prefer spending a bit more when they felt the product’s quality was worth it. And, overall, the average sales rate was an impressive 211.78%, showing strong customer interest throughout the year.
