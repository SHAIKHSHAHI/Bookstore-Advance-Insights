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

### 1.Sales and Revenue Analysis

**Objective:** Analyze yearly sales revenue and quantity sold.
**Output:**
- 📦 Extracted yearly total revenue and quantity sold from the `Orders` table using SQL aggregation.
- 📊 Plotted the results to visualize:
  - Annual revenue trends.
  - Yearly sales quantity.
  - Comparison between revenue and quantity sold.
  - Revenue share per year using a pie chart.

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

### 2.📚 Genre-Wise Borrowing Trends Analysis Over the Years

- Extracted genre-wise data from the Orders and Books tables using SQL:
- Fetched distinct book count and total orders for each genre per year.


Visualized the insights using two plots:

📊 Bar Plot showing unique books borrowed by genre, across years.

📈 Line Plot showing total number of orders placed per genre, over time.

```sql
select b.Genre,
       year(a.Order_Date) as Year,
       count(Distinct a.Book_ID) as Book_Count,
       count(Distinct a.Order_ID) as Total_Orders
from Orders as a
join Books as b
on a.Book_ID = b.Book_ID
group by year(Order_Date), b.genre
order by Book_Count;
```
```Python
# Matplotlib & Seaborn Visualization
plt.figure(figsize=(8,10), dpi=300)

# Bar Plot - Unique Books by Genre
plt.subplot(2,1,1)
sns.barplot(data=Genre_Books_Count,
x='Genre', y='Book_Count', hue='Year',
palette='Dark2', saturation=0.75)
plt.title("Unique Book Borrowings by Genre Over the Years")

# Line Plot - Orders by Genre
plt.subplot(2,1,2)
sns.lineplot(data=Genre_Books_Count, x='Genre',
 y='Total_Orders', hue='Year', style='Year',
 palette='flare')
plt.title("Total Orders Placed Genre-Wise Over the Years")

plt.tight_layout()
plt.savefig('Genres Trend.png')
plt.show()
```
![Genre-Wise Trends](Genres%20Trend.png)

## 3. 🧑‍🤝‍🧑 Customer Segment and Trend Analysis

- 1.Extracted only customers who placed at least one order by joining the Customers and Orders tables.
- 2.Queried year-wise count of unique customers to analyze growth over time.
- 3.Retrieved Top 10 countries based on total number of unique customers.

**1.Identified:**

- 1. Regular Customers: who placed orders in 2 or more different years.
- 2.Irregular Customers: who placed orders in only one year.


**2.Segmented customers into 4 categories based on their total spend and order count:**

🏆 Premium: Spent ≥ 800

🔁 Regular: Spent ≥ 500

☝️ One Time Buyer: Only 1 order

🪙 Low Spender: Everyone else




**3.Aggregated segment-wise revenue and quantity sold for each year using CTE and joins.**

**Visualized:**

📊 Top 10 countries by customer count using bar chart.
📈 Year-wise unique customers using bar chart.
🧮 Comparison of Regular vs Irregular customers using horizontal bar chart.
🔥 Revenue by Customer Segment across years using heatmap.


**4.Saved final visualization as CustomerSegment.png.**

```sql

UniqueCustomers_Count="""
select count(Distinct a.Customer_ID)as
Customer_Count,
year(b.Order_Date)as Year
From Customers as a
join Orders as b
on a.Customer_ID=b.Customer_ID
group by year(b.Order_Date)"""

Yearly_UniqueCustomers=pd.read_sql(UniqueCustomers_Count,conn)
print(Yearly_UniqueCustomers)

Top10_Customer_Countries="""
select count(Distinct Customer_ID)as 
Customer_Count,Country
from Customers
Group by Country
order by Customer_Count desc
limit 10"""
CustomerCount_CountryTop10=pd.read_sql(Top10_Customer_Countries,conn)
print(CustomerCount_CountryTop10)

Regular_Customers_Count="""
select 
count(Customer_ID)
as Regular_Customers
from (
select  Customer_ID
from Orders
Group by Customer_ID
Having count(Distinct year(Order_Date))>=2
)ct"""

Regular_Customers=pd.read_sql(Regular_Customers_Count,conn)
print(Regular_Customers)

Irregular_Customers_Count = """
SELECT 
    COUNT(DISTINCT Customer_ID) AS Irregular_Customers
FROM Customers 
WHERE Customer_ID IN (
    SELECT Customer_ID
    FROM Orders
    GROUP BY Customer_ID
    HAVING COUNT(DISTINCT YEAR(Order_Date)) = 1
)
"""
Irregular_Customers=pd.read_sql(Irregular_Customers_Count,conn)
print(Irregular_Customers)

Customer_Segment_Revenue="""
with CustomerSegment as (
select
Customer_ID,
count(Order_ID)as Order_Count,
sum(Total_Amount) AS Total_Spent,
case
        when sum(Total_Amount) >= 800 then 'Premium'
        when sum(Total_Amount) >= 500 then 'Regular'
        when count(Order_ID)=1
        then 'One Time Buyer'
        else 'Low Spender'
end AS CustomerSegment
from Orders
group by Customer_ID)

select sum(b.Total_amount) as Customer_Revenue,
sum(b.Quantity)as Quantity,
a.CustomerSegment,
year(b.Order_Date)as Year
from CustomerSegment as a
join Orders as b
on a.Customer_ID=b.Customer_ID
group by year(b.Order_Date),CustomerSegment
order by Year,CustomerSegment
"""
Customer_Categories_Revenue= pd.read_sql(Customer_Segment_Revenue,conn)
print(Customer_Categories_Revenue)

regular=Regular_Customers['Regular_Customers'][0]
Irregular=Irregular_Customers['Irregular_Customers'][0]

categories = ['Regular Customers', 'Irregular Customers']
counts = [regular, Irregular]

```
```python
plt.figure(figsize=(15,12),dpi=300)

plt.subplot(2,2,1)

sns.barplot(data=CustomerCount_CountryTop10,
            x='Customer_Count',
            y='Country',
            palette='crest')

plt.title('Top10_Countries Based on Customers', fontsize=14, fontweight='heavy')
plt.xlabel('Number of Unique Customers', fontsize=14, fontweight='heavy')
plt.ylabel('Country', fontsize=14, fontweight='heavy')
plt.grid(True, linestyle='--', alpha=0.6)


# Subplot 1: Lineplot
plt.subplot(2,2,2)

sns.barplot(data=Yearly_UniqueCustomers, 
            x='Year', 
            y='Customer_Count', 
            palette='flare',
            width=0.8)

plt.title('Year-wise Unique Customers', fontsize=14, fontweight='heavy')
plt.xlabel('Year', fontsize=14, fontweight='heavy')
plt.ylabel('Customer Count', fontsize=14, fontweight='heavy')

plt.grid(axis='x', linestyle='--', alpha=0.5)


plt.subplot(2,2,3)

sns.barplot(y=categories, x=counts, palette='flare')
plt.title('Customer Count Based Types ', fontsize=14, fontweight='bold')
plt.xlabel('Customer Type',fontsize=14, fontweight='heavy')
plt.ylabel('Total Count',fontsize=14, fontweight='heavy')

plt.grid(axis='x', linestyle='--', alpha=0.6)

plt.subplot(2,2,4)

pivot = Customer_Categories_Revenue.pivot(index='CustomerSegment', columns='Year', values='Customer_Revenue')
sns.heatmap(pivot, annot=True, cmap='crest', fmt=".0f")
plt.title("Revenue By Customer Segment and Year",fontsize=14, fontweight='heavy')
plt.xlabel('Year',fontsize=14, fontweight='heavy')
plt.ylabel('CustomerSegment',fontsize=14, fontweight='heavy')
plt.xticks(rotation=30)
plt.yticks(rotation=30)

plt.tight_layout(rect=[1,1,1,3])  # Adjust spacing to make room
plt.suptitle("Customer Segment and Customer Trend Analysis",
fontsize=20,fontweight='heavy')
plt.subplots_adjust(hspace=0.5, wspace=0.5)
plt.savefig('CustomerSegment.png')
```


plt.show()

![Customer Segment Trend](CustomerSegment.png)
## 4. 📈 Borrowing Trend Analysis
1.Extracted top 3 trending books by genre in 2024 based on total quantity ordered .
2.Extracted monthly borrowing event counts for 2024 from Orders.
## Visuals
1.Created a bar plot comparing stock vs total quantity ordered for the top 3 books per genre.
2.Created a line plot showing the monthly borrowing events trend in 2024.

![ Borrowing Trend](Borrowing%20Trend.png)

## 📌 Conclusion

This project leverages SQL to deliver actionable insights into bookstore sales, customer behavior, and inventory management.  
The analysis provides a clear understanding of market trends and opportunities for strategic decision-making.  
Overall, it serves as a valuable tool to enhance business performance and growth.
