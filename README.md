# SQL Sales Performance Analysis 🗄️

## 📌 Project Overview
Analysed 9,800 rows of Superstore sales data using SQL Server Management Studio 
to uncover key business insights around revenue, customer behaviour and product performance.

## 🛠️ Tools Used
- SQL Server Management Studio (SSMS)
- SQL (T-SQL)

## 📂 Dataset
- Source: Kaggle — Superstore Sales Dataset
- 9,800 rows of transactional sales data

## ❓ Business Questions Answered
1. Which product category generates the most revenue?
2. Which region has the highest sales?
3. Who are the top 10 customers by total spend?
4. Which month had the best sales performance?
5. What is the average order value per region?
6. Which sub-categories have the lowest sales performance?
7. Which customer segment drives the most orders?

## 📊 SQL Queries

### 1. Total Sales by Category
```sql
SELECT 
    Category,
    ROUND(SUM(TRY_CAST(Sales AS FLOAT)), 2) AS Total_Sales
FROM superstore_data
GROUP BY Category
ORDER BY Total_Sales DESC;
```

### 2. Total Sales by Region
```sql
SELECT 
    Region,
    ROUND(SUM(TRY_CAST(Sales AS FLOAT)), 2) AS Total_Sales
FROM superstore_data
GROUP BY Region
ORDER BY Total_Sales DESC;
```

### 3. Top 10 Customers by Total Spend
```sql
SELECT TOP 10
    Customer_Name,
    ROUND(SUM(TRY_CAST(Sales AS FLOAT)), 2) AS Total_Spent
FROM superstore_data
GROUP BY Customer_Name
ORDER BY Total_Spent DESC;
```

### 4. Monthly Sales Trend
```sql
SELECT 
    SUBSTRING(Order_Date, 7, 4) + '-' + SUBSTRING(Order_Date, 4, 2) AS Month,
    ROUND(SUM(TRY_CAST(Sales AS FLOAT)), 2) AS Monthly_Sales
FROM superstore_data
GROUP BY SUBSTRING(Order_Date, 7, 4) + '-' + SUBSTRING(Order_Date, 4, 2)
ORDER BY Month;
```

### 5. Average Order Value by Region
```sql
SELECT 
    Region,
    ROUND(AVG(TRY_CAST(Sales AS FLOAT)), 2) AS Avg_Order_Value
FROM superstore_data
GROUP BY Region
ORDER BY Avg_Order_Value DESC;
```

### 6. Low Performing Sub-Categories
```sql
SELECT 
    Sub_Category,
    ROUND(SUM(TRY_CAST(Sales AS FLOAT)), 2) AS Total_Sales,
    COUNT(*) AS Number_Of_Orders
FROM superstore_data
WHERE TRY_CAST(Sales AS FLOAT) < 50
GROUP BY Sub_Category
ORDER BY Total_Sales ASC;
```

### 7. Customer Segment JOIN Analysis
```sql
SELECT 
    c.Customer_Name,
    c.Segment,
    ROUND(SUM(TRY_CAST(s.Sales AS FLOAT)), 2) AS Total_Sales,
    COUNT(*) AS Number_Of_Orders
FROM superstore_data s
JOIN customers c ON s.Customer_ID = c.Customer_ID
GROUP BY c.Customer_Name, c.Segment
ORDER BY Total_Sales DESC;
```

## 💡 Key Insights
- Technology was the highest revenue category
- West region leads in total sales
- Sean Miller is the top spending customer at $25,043
- Sales peak in November and December every year
- Fasteners is the lowest performing sub-category

## 🔗 Full Project Write-Up
[View on Notion Portfolio](https://merciful-coconut-e1f.notion.site/Ompha-Ramaru-Data-Analyst-Portfolio-3498a09bc57780a8851ed774fa74d0b6)
