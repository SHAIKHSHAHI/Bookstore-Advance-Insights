# 📚 Bookstore Sales Insights: Advanced SQL Analysis & Data Exploration

---

## 📖 Project Overview

This project dives deep into bookstore transaction data using advanced SQL queries.  
We explore sales patterns, customer behavior, and genre preferences.  
It provides actionable insights based on real-world data structures.

---

## 🎯 Project Objectives

- ✅ Perform monthly and yearly sales & revenue analysis  
- ✅ Identify top-selling books by genre and author  
- ✅ Segment customers based on location and purchasing behavior  
- ✅ Analyze borrowing patterns over different periods  
- ✅ Evaluate inventory stock vs. demand for better planning  
- ✅ Spot genre trends and seasonal fluctuations  
- ✅ Detect customer engagement through repeat orders  
- ✅ Discover revenue contribution by customer location.

---

## 🛠️ Tools Used

- 🗃️ MySQL – to write and run SQL queries for data exploration  
- 📊 Seaborn – for optional visual representation of trends  
- 📈 Matplotlib – for professional plotting (if needed)

---


## 📁 Project Structure

```
bookstore-sql-insights/
│
├── README.md                     → Project documentation and overview
├── SQL_Queries/                  → SQL scripts for all analyses
│   ├── sales_revenue_analysis.sql
│   ├── customer_segment_analysis.sql
│   ├── genre_trend_analysis.sql
│   └── borrowing_analysis.sql
├── Data/                         → Contains raw CSV files
│   ├── books.csv                 → 500 rows × 7 columns  
│   ├── orders.csv                → 500 rows × 6 columns  
│   └── customers.csv             → 500 rows × 6 columns  
├── Reports/                      
└── Visuals/                
```
## 📊 Key Insights

- 📅 Tracked monthly and yearly sales trends using order data.  
- 🧾 Identified top-selling books and high-revenue genres.  
- 👥 Segmented customers by location for regional insights.  
- 🔁 Found repeat buyers and high-frequency customers.  
- 📚 Highlighted low-stock, high-demand books for restocking.  
- 🕵️‍♀️ Observed changing genre preferences over time.  
- 💰 Analyzed key revenue drivers across products and customers.  
- 📈 Showcased consistent growth in orders and revenue.

- 
---

## 🔄 Data Analysis Workflow - Key Points

- Performed all data querying and analysis directly in MySQL using optimized SQL queries.  
- Extracted valuable insights from the `Books`, `Orders`, and `Customers` tables through SQL commands.  
- Established a connection between Python and MySQL to fetch query results for further use.
- Created clear and informative visualizations of sales trends and customer segments using `matplotlib` and `seaborn`.  

---

### 1️⃣ Sales and Revenue Analysis

**Objective:** Analyze yearly sales revenue and quantity sold.

```sql
SELECT YEAR(Order_Date) AS Year, 
       SUM(Total_Amount) AS Yearly_Revenue, 
       SUM(Quantity) AS Yearly_SalesQuantity
FROM Orders
GROUP BY YEAR(Order_Date)
ORDER BY Year```

## 📌 Conclusion

This project leverages SQL to deliver actionable insights into bookstore sales, customer behavior, and inventory management.  
The analysis provides a clear understanding of market trends and opportunities for strategic decision-making.  
Overall, it serves as a valuable tool to enhance business performance and growth.
