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
ORDER BY Year
```
---
```python
plt.figure(figsize=(10, 14),dpi=300)

plt.subplot(2,2,1)
sns.lineplot(data=Yearly_Revenue_Quantity, x='Year', y='Yearly_Revenue',
             marker='o', color='purple')
plt.grid(True, linestyle='--', linewidth=1, alpha=0.7)
plt.title('Revenue Generated Per Year', fontsize=12, fontweight='heavy', fontstyle='italic')
plt.xlabel('Year', fontsize=12, fontweight='heavy')
plt.ylabel('Revenue', fontsize=12, fontweight='heavy')
plt.xticks(Yearly_Revenue_Quantity['Year'],rotation=20)

plt.subplot(2,2,2)
sns.barplot(data=Yearly_Revenue_Quantity, x='Year', y='Yearly_SalesQuantity',
            palette='flare', alpha=0.8)
plt.title('Quantity Sold Per Year', fontsize=12, fontweight='heavy', fontstyle='italic')
plt.xlabel('Year', fontsize=12, fontweight='heavy')
plt.ylabel('Sales Quantity', fontsize=12, fontweight='heavy')
plt.xticks(rotation=20)


plt.subplot(2,2, 3)
sns.scatterplot(data=Yearly_Revenue_Quantity, x='Yearly_SalesQuantity', y='Yearly_Revenue', hue='Year', palette='flare', s=200)
plt.title('Comparison of Quantity Sold and Revenue Earned', fontsize=12, fontweight='heavy', fontstyle='italic')
plt.xlabel('Sales Quantity', fontsize=12, fontweight='heavy')
plt.ylabel('Total Revenue', fontsize=12, fontweight='heavy')
plt.legend(title='Year')

plt.suptitle("Annual Wise Sales and Revenue Trend", fontsize=20, fontweight='heavy')
plt.subplots_adjust(hspace=0.4)

plt.subplot(2, 2, 4)
plt.pie(Yearly_Revenue_Quantity['Yearly_Revenue'], labels=Yearly_Revenue_Quantity['Year'],
        colors=['pink','orange','coral'], autopct='%1.0f%%', shadow=True,radius=1.5,
        textprops={'fontsize': 12, 'color': 'black', 'weight': 'bold'},
        wedgeprops={'edgecolor': 'black', 'linewidth': 2,'width':0.8})
plt.title('Revenue Contribution by Year', fontsize=12, fontweight='heavy', fontstyle='italic')
plt.legend(title='year',loc='lower right')


plt.tight_layout(rect=[1,1,1,3])  
plt.suptitle("Annual Wise Sales and Revenue Trend", fontsize=20, fontweight='heavy')
plt.subplots_adjust(hspace=0.5, wspace=0.5)
plt.savefig('Sales And Revenue Analysis.png')


plt.show()
```

![Sales and Revenue Analysis](Sales%20And%20Revenue%20Analysis.png)


## 📌 Conclusion

This project leverages SQL to deliver actionable insights into bookstore sales, customer behavior, and inventory management.  
The analysis provides a clear understanding of market trends and opportunities for strategic decision-making.  
Overall, it serves as a valuable tool to enhance business performance and growth.
