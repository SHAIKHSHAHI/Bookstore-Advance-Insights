![Booksstore](caption.jpg)
# 📚 Bookstore Sales Insights: Advanced SQL Analysis & Data Exploration

---

## 📖 Project Overview

### This project dives deep into bookstore transaction data using advanced SQL queries.  
### We explore sales patterns, customer behavior, and genre preferences.  
### It provides actionable insights based on real-world data structures.

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


# Key Values
```python
AvgQuantity_Per_Order
                5.394
   Total_Quantity_ordered
                2697.0
   Total_Revenue_Generated
                75628.66
```

# 📋 Basic Queries
## 🌟 Code 1:  Unique Customer Count Analysis
```python
UniqueCustomers="""
select count(Distinct a.Customer_ID)as
UniqueCustomer_Count
From Customers as a
join Orders as b
on a.Customer_ID=b.Customer_ID

UniqueCustomers_Count=pd.read_sql(UniqueCustomers,conn)
print(UniqueCustomers_Count)
```
 

## 🌟 Code 2: Unique Cities Count
```python

City_Count="""select count(Distinct City)as Cities
from Customers"""
CitiesCount=pd.read_sql(City_Count,conn)
print(CitiesCount)
```
 

## 🌟 Code 3: 📅 Distinct Order Years
```python
Order_Years="""
select Distinct
(extract(year from Order_Date))as years from Orders
Order by years"""
Orders_Placed_Years=pd.read_sql(Order_Years,conn)
print(Orders_Placed_Years)
```



## 🌟 Code 4: 👥 Customers Per Year
```python
CustomersPerYear="""
select count(Distinct Customer_ID)as Customers_Per_Year ,
year(Order_Date)as Order_Year
from Orders
group by Order_Year
Order by Order_Year
"""
Yearly_Customers= pd.read_sql(CustomersPerYear, conn)
print(Yearly_Customers)
```

## 🌟 Code 5: 📚 Total Unique Books Available
``` python
TotalUniqueBooks="""
select count(Distinct Book_ID)as Book_Count
from Books"""
TotalBooksAvailable=pd.read_sql(TotalUniqueBooks,conn)
print(TotalBooksAvailable)
```
📌 Explanation:

✅ This query counts the total number of unique books present in the Books table.

✅ Useful for knowing the overall size of the book inventory.


## 🌟 Code 6: 📦 Total Quantity Ordered
```python
TotalUniqueBooks="""
select count(Distinct Book_ID)as Book_Count
from Books"""
TotalBooksAvailable=pd.read_sql(TotalUniqueBooks,conn)
print(TotalBooksAvailable)
```
## 🌟 Code 7: 📊 Average Quantity Sold
```python
AverageQuantitySold="""
select avg(Quantity)as avg_Quantiy
from Orders"""
AvgQuantity=pd.read_sql(AverageQuantitySold,conn)
print(AvgQuantity)
```
## 🌟 Code 8: 📅 Total Orders Placed Per Year
```python
OrdersPerYear="""
select year(Order_Date)as Year,count(Distinct Order_ID)as Total_Orders
from Orders
group by year(Order_Date)
"""
YearlyOrders=pd.read_sql(OrdersPerYear,conn)
print(YearlyOrders)
```
```plaintext
Year  Total_Orders
0  2022            16
1  2023           256
2  2024           228
```

## 🌟 Code 9: 💰 Total Sales Generated Per Year
```python
SalesPerYear="""
select year(Order_Date)as Year,sum(Total_Amount)as Total_Sales
from Orders
group by year(Order_Date)
"""
YearlySales=pd.read_sql(SalesPerYear,conn)
print(YearlySales)
```
## 🌟 Code 10: 📚 List of Distinct Book Genres
```python
Genres="""
select Distinct Genre from
Books
"""
Distinct_Genres=pd.read_sql(Genres,conn)
print(Distinct_Genres)
```
```plaintext
0        Biography
1          Fantasy
2      Non-Fiction
3          Fiction
4          Romance
5  Science Fiction
6          Mystery
```
## 🌟 Code 11: ✍️ Count of Unique Authors in the Dataset
```python
Authors="""
select count(Distinct Author)as
Authors_Count from 
Books
"""
Author_Count=pd.read_sql(Authors,conn)
print(Author_Count)
```
```plaintext
Authors_Count
0            493
```
## 🌟 Code 12: 💰 Average Book Price Calculation
```python
AvgBookPrice="""select avg(price)as avg_BookPrice
from Books"""
AvgPrice= pd.read_sql(AvgBookPrice,conn)
```

## 🌟 Code 13: 💵 Total Revenue Generated
```python
Total_Revenue="""select sum(Total_Amount)as Total_Revenue_Generated
from Orders"""
TotalRevenue=pd.read_sql(Total_Revenue,conn)
print(TotalRevenue)
```
# Advance Queries 📊 | Powerful Insights Through Complex SQL

## 🌟 Code 14: 🏆 Top 10 Customers Based on Orders Placed
```python
Top10Customers_OrdersBased="""
Select a.Customer_ID as Customer,
count(Distinct b.Order_ID)as Orders_placed
from Customers as a
join Orders as b
on a.Customer_ID =b.Customer_ID
group by a.Customer_ID
order by Orders_placed desc
limit 10
"""
Top10_OrderedCustomers=pd.read_sql(Top10Customers_OrdersBased,conn)
print(Top10_OrderedCustomers)
```
📌 Explanation:

✅ This SQL query identifies the top 10 customers who have placed the highest number of unique orders.

✅ It uses JOIN to combine customer and order data.

✅ COUNT(DISTINCT Order_ID) ensures only unique orders are counted.

✅ ORDER BY Orders_placed DESC ranks them in descending order.

✅ This helps analyze loyalty and engagement of high-value customers.

## 🌟 Code 15: 👤 Count of One-Time Customers
```python
One_Time_Customers = """
SELECT
COUNT(Distinct Customer_ID) AS One_Time_Customers
FROM Customers
WHERE Customer_ID IN (
SELECT Customer_ID
FROM Orders
GROUP BY Customer_ID
HAVING COUNT(Distinct Order_ID) = 1
)
"""
One_Time_Customers_Count=pd.read_sql(One_Time_Customers,conn)
print(One_Time_Customers_Count)
```
📌 Explanation:

✅ This query counts customers who placed only one order ever.

✅ Helpful in identifying low-retention or casual buyers.


✅ Uses a subquery to filter customers with exactly 1 unique order.

## 🌟 Code 16: 🔁 Count of Repeated Customers
```python
Repeated_Customers = """
SELECT 
    COUNT(Distinct Customer_ID) AS Repeated_Customers
FROM Customers 
WHERE Customer_ID IN (
    SELECT Customer_ID
    FROM Orders
    GROUP BY Customer_ID
    HAVING COUNT(Distinct Order_ID) > 1
)
"""
Repeated_Customers_Count=pd.read_sql(Repeated_Customers,conn)
print(Repeated_Customers_Count)
```
📌 Explanation:

✅ This query finds customers who have placed more than one order.

✅ Helps identify loyal or returning customers.

✅ Useful for tracking customer retention trends.

```plaintext
One-time vs Repeated Customers
One_Time_Customers = 168
Repeated_Customers = 139
```
## 🌟 Code 17: 💰 Top 10 Customers Based on Total Spending
```python
Top10Customers_SpendingBased="""
Select  a.Customer_ID as Customer,
sum(b.Total_Amount)as Total_Spent
from Customers as a
join Orders as b
on a.Customer_ID =b.Customer_ID
group by a.Customer_ID
order by  Total_Spent desc
limit 10
"""
Top10_SpendingCustomers=pd.read_sql(Top10Customers_SpendingBased,conn)
print(Top10_SpendingCustomers)
```
```plaintext
# Customers with Highest Total Spending
Top_Spending_Customers = {
    457: 1398.90,
    174: 1080.95,
    364: 1052.27,
    405: 991.00,
    386: 986.30,
    425: 942.62,
    474: 929.19,
    163: 746.65,
    167: 719.93,
    214: 682.15
}
```
📌 Explanation:

✅ This SQL query retrieves the top 10 customers who have spent the most.

✅ It joins Customers and Orders tables to sum total amount spent.

✅ Helps businesses recognize their highest-value customers.

✅ Useful for loyalty programs and customer engagement strategies.

✅ Data is grouped by Customer_ID and sorted in descending order.

## 🌟 Code 18: 🏙️ Top 10 Cities with Highest Customer Count
```python
Top10CustomersCities="""
select City,count(Distinct Customer_ID)
as Customer_Count
from Customers 
group by City
Order by Customer_Count desc
limit 10"""
Country_CustomerCount=pd.read_sql(Top10CustomersCities,conn)
print(Country_CustomerCount)
```
📌 Explanation:

✅ This query finds the top 10 cities with the most unique customers.

✅ Helps identify geographical hotspots where customer base is concentrated.

✅ Groups customer data by city and counts distinct Customer_ID.

✅ Insightful for targeted marketing and regional campaigns.

✅ Data is sorted in descending order by customer count.

✅ Supports location-wise customer segmentation.

## 🌟 Code 19: ❌ Churned/Inactive Customers Before 2024
```python
Churned_Customers="""select Customer_ID,
Max(Order_Date)as Last_Order
from Orders
Group by Customer_ID
Having year(Last_Order)<2024
"""
Inactive_Customers= pd.read_sql(Churned_Customers, conn)
print(Inactive_Customers)
```
📌 Explanation:

✅ This query identifies churned customers—those who haven’t placed any orders in 2024.

✅ It retrieves each customer's latest order date.

✅ Filters out customers whose last purchase was before 2024.

✅ Helps in understanding customer retention and targeting re-engagement campaigns.

✅ Valuable for calculating churn rate in business performance analysis.

✅ Result: a list of customers considered inactive or lost.

## 🌟 Code 20: 🆕 Most Recent Customer Details
```python
Recent_Customer="""
select a.Customer_ID ,
a.Order_Date,
b.Name,
b.Country
,b.City
from Orders as a
join Customers as b
on a.Customer_ID=b.Customer_ID
order by a.Order_Date Desc
limit 1"""
RecentCustomer= pd.read_sql(Recent_Customer, conn)
print(RecentCustomer)
```

📌 Explanation:

✅ This query fetches the most recent customer who placed an order.

✅ It includes details like Customer ID, Order Date, Name, Country, and City.

✅ Uses ORDER BY Order_Date DESC to sort from latest to oldest.

✅ LIMIT 1 ensures only the latest customer is retrieved.

✅ Helps identify who was the last active buyer on the platform.

✅ Useful for recent engagement analysis or real-time dashboards.

## 🌟 Code 21: 🥇 First Customer Details
```python
First_Customer="""
select a.Customer_ID ,
a.Order_Date,
b.Name,
b.Country
,b.City
from Orders as a
join Customers as b
on a.Customer_ID=b.Customer_ID
order by a.Order_Date
limit 1"""
FirstCustomer= pd.read_sql(First_Customer, conn)
print(FirstCustomer)
```
📌 Explanation:

✅ This query retrieves the first-ever customer who placed an order.

✅ Displays key information like Customer ID, Order Date, Name, Country, and City.

✅ Uses ORDER BY Order_Date to sort from earliest to latest.

✅ LIMIT 1 ensures only the first customer is selected.

✅ Helpful in understanding early adopters and customer journey beginnings.

✅ Can be used in historical analysis and platform growth tracking.

## 🌟 Code 22: 📚 Published Year Range of Books
```python
Published_Years_Range="""
with Earliest as
(select Published_Year as year 
from Books
 order by Published_Year asc
  limit 1) ,
Latest as
(select Published_Year as year from Books 
order by Published_Year desc
 limit 1)
select
(select year from Earliest ) as Earliest_year,
(select year from  Latest )as Latest_year
"""
PublishedYearsRange=pd.read_sql(Published_Years_Range,conn)
print(PublishedYearsRange)
```

📌 Explanation:

✅ This query fetches the earliest and latest published year of all books.

✅ Uses two CTEs: Earliest and Latest to find minimum and maximum years.

✅ LIMIT 1 with ORDER BY ensures only the top record is selected.

✅ Returns a single row with Earliest_year and Latest_year.

✅ Useful for understanding the publication span of your book catalog.

✅ Helpful in tracking how recent or historical your inventory is.

## 🌟 Code 23: 🕰️ Old vs Latest Books Count
```python
Old_Books_Count="select count(Book_ID) from Books where Published_Year=1990"
OldBooks=pd.read_sql(Old_Books_Count,conn)
print(OldBooks)

Latest_Books_Count="select count(Book_ID) from Books where Published_Year=2003"
LatestBooks=pd.read_sql(Latest_Books_Count,conn)
print(LatestBooks)
```
📌 Explanation:

✅ This query fetches the earliest and latest published year of all books.

✅ Uses two CTEs: Earliest and Latest to find minimum and maximum years.

✅ LIMIT 1 with ORDER BY ensures only the top record is selected.

✅ Returns a single row with Earliest_year and Latest_year.

✅ Useful for understanding the publication span of your book catalog.

✅ Helpful in tracking how recent or historical your inventory is.

## 🌟 Code 24: 📦 Book Stock Level Classification
```python
Stock_Status="""
select Book_ID,
sum(Stock),
    case  
        when sum(Stock) is not null and
        sum(Stock) != 0 and sum(Stock)<10 then 'Understock'
        when sum(Stock)>50 then 'Overstock'
        Else 'Optimum Stock'
    end as Stock_Status
from Books
group by Book_ID 
"""
Stocks=pd.read_sql(Stock_Status,conn)
print(Stocks)
```
📌 Explanation:

✅ This query groups books by Book_ID and calculates total stock.

✅ Then it classifies stock into three categories: Understock, Overstock, and Optimum Stock.

✅ Understock → stock < 10, Overstock → stock > 50, else optimum.

✅ Helps in inventory planning, highlighting books that need restocking or clearance.

✅ Great for maintaining stock efficiency and balance.

## 🌟 Code 25: 💸 Book Price Segmentation
```python
Book_Segment="""select 
Book_ID,
Price,
case
        when Price >=30 then 'premium'
        when Price <30 then 'cheaper'
end as BookSegment
from Books"""
Book_Seg= pd.read_sql(Book_Segment,conn)
print(Book_Seg)
```
📌 Explanation:

✅ This query categorizes each book based on its price.

✅ Books priced ₹30 or above are labeled as "premium".

✅ Books priced below ₹30 are labeled as "cheaper".

✅ Helps in price-based customer targeting and inventory grouping.

## 🌟 Code 26: 👤 Customer Segmentation Based on Spending in 2024
```python
Customer_Segment="""select
Customer_ID,
sum(Total_Amount) AS Total_Spent,
case
        when sum(Total_Amount) >= 800 then 'Premium'
        when sum(Total_Amount) >= 500 then 'Regular'
        else 'Low Spender'
end AS CustomerSegment
from Orders
where year(Order_Date)=2024
group by Customer_ID
"""
CustomerSegment= pd.read_sql(Customer_Segment,conn)
print(CustomerSegment)
```
📌 Explanation:

✅ This query classifies customers into segments by their total spending in the year 2024.

✅ Segments:

Premium (spent ₹800 or more)

Regular (spent ₹500–₹799)

Low Spender (spent less than ₹500)


✅ Useful for targeted marketing and loyalty strategies.

## 🌟 Code 27: 📊 Monthly Borrowing Trend Comparison (2023 vs 2024)
```python
Monthly_Borrowing_2024 = """
SELECT
MONTHNAME(Order_Date) AS Month,
COUNT(DISTINCT Order_ID) AS Borrowing_Events_2024
FROM Orders
WHERE EXTRACT(YEAR FROM Order_Date) = 2024
GROUP BY MONTHNAME(Order_Date), EXTRACT(MONTH FROM Order_Date)
ORDER BY EXTRACT(MONTH FROM Order_Date)
"""
Monthly_Analysis2024 = pd.read_sql(Monthly_Borrowing_2024, conn)
print(Monthly_Analysis2024)

Monthly_Borrowing_2023 = """
SELECT
MONTHNAME(Order_Date) AS Month,
COUNT(DISTINCT Order_ID) AS Borrowing_Events_2023
FROM Orders
WHERE EXTRACT(YEAR FROM Order_Date) = 2023
GROUP BY MONTHNAME(Order_Date), EXTRACT(MONTH FROM Order_Date)
ORDER BY EXTRACT(MONTH FROM Order_Date)
"""
Monthly_Analysis2023= pd.read_sql(Monthly_Borrowing_2023, conn)
print(Monthly_Analysis2023)

Monthly_Trend_Comparison = pd.merge(
Monthly_Analysis2023 ,
Monthly_Analysis2024,
on='Month',
how='outer'
).fillna(0)
print(Monthly_Trend_Comparison)
```
📌 Explanation:

✅ This code compares monthly borrowing activity for the years 2023 and 2024.

✅ It calculates the number of distinct borrowings (Order_IDs) for each month in both years.

✅hen merges both datasets to form a single trend comparison table.

✅ Helps identify seasonal borrowing behavior and growth/drop patterns month-wise.

✅ Ideal for plotting a line/bar chart to visualize shifts in customer engagement.



# 📊 Visualisations & Interpretation of Output/Results

- Visuals such as bar charts, line graphs, and pie charts were used to present trends clearly.

- Sales, customer segments, and genre-wise performance were visualized for better insights.

- Charts helped identify seasonal trends, top-performing books, and customer behavior.

- Understock and overstock patterns were highlighted using conditional formatting and counts.

- Year-wise comparison showed clear growth in low spender segments and one-time buyers.

- Interpretations drawn from visuals guided meaningful business recommendations and actions.


```plaintext
Book_ID | Stock | Years Ordered | Quantity | Orders | Price
------------------------------------------------------------
60      | 0     | 1             | 9        | 1      | 35.14
127     | 0     | 3             | 9        | 3      | 11.66
163     | 0     | 1             | 3        | 1      | 19.11
378     | 0     | 1             | 6        | 1      | 6.01
```
## 1. Out of Stock Books

🧠 Insights:

-📉 Low order frequency (1–3 orders only).

- Still out of stock, meaning initial stock was very small.

- 📊 These books didn’t sell a lot, so stock may have never been replenished.

- ⚠️ May need better inventory planning or reorder automation.

```plaintext
Book_ID | Stock | Quantity | Orders | Price
--------------------------------------------
105     |   85  |     12    |   6    |  25.99
212     |   90  |     5     |   3    |  19.50
337     |   72  |     7     |   4    |  22.75
418     |   95  |     2     |   1    |  30.00
129     |   88  |     9     |   3    |  15.60
222     |   76  |     4     |   2    |  18.20
301     |   99  |     1     |   1    |  34.10
456     |   82  |     6     |   3    |  27.00
199     |   74  |     8     |   4    |  20.00
388     |   79  |     3     |   2    |  215
```
## 2. Overstocked Books (Stock > 70)

Mostly only 1–2 orders per book.

Low quantity per order (some just 1–3 units).

### 🧠 Insights:

📈 Over-purchased, but not in demand.

🛒 Needs promotion, or stop ordering those not performing.

## 3. Low Stock (Stock ≤ 10)
```plaintext
Book_ID | Stock | Quantity | Orders | Price
--------------------------------------------
390     |   1   |     15    |   6    |  13.99
287     |   2   |     22    |   9    |  10.50
128     |   1   |     18    |   7    |  11.25
145     |   2   |     25    |   8    |  16.40
319     |   1   |     20    |   6    |  12.00
204     |   2   |     17    |   7    |  14.30
277     |   1   |     19    |   5    |  15.80
342     |   2   |     21    |   9    |  11.90
411     |   1   |     23    |   6    |  10.75
151     |   2   |     24    |   8    |  13.60
```

## 1.📦 Stock Status & Order Frequency Analysis

- Books were classified as Overstocked, Understocked, or Stockout based on inventory levels.

- The Quantity column was used to assess whether high sales frequency contributed to stock shortages.

- Book_ID helped identify specific books that frequently faced stock issues.

- This insight enables businesses to perform a deeper performance analysis on these titles.

- Understanding stock patterns helps in planning inventory strategies more effectively.

- Actionable steps like reordering fast-moving titles or reducing overstock can optimize operations

## 2.📊 Customer Segment Analysis – Revenue Trends
![CustomerSegment](Customer%20Segment%20(1).png)

- Customers were segmented into Premium, Regular, and Low Spender based on total spending across 3 years.

- Interestingly, Low Spender segment contributed the highest revenue in 2024, despite having the lowest cumulative revenue earlier (only 585).

- No premium customers existed in 2022, indicating no high spenders during that year.

- Across all years, Premium Segment consistently generated the lowest revenue, showing fewer high-value buyers.

- One-time buyers played a key role — their contribution grew from 1,201 (2022) to 11,849 (2024).

- Regular customers showed a dip in 2024, from 8,451 to 7,472, requiring attention.

- The business should implement strategies to retain one-time buyers and convert them into repeat or premium customers.

# 📌 Recommendations

Reduce purchase of overstocked books with low demand.

Restock books that are out of stock but in high demand.

Monitor past order quantity to plan stock effectively.

Set alerts for books with critically low stock.

Use discounts/offers to clear excess inventory.

Revisit pricing of books with low sales.

Avoid overstocking slow-moving titles.

Focus on books with higher order frequency.

Manage stock based on customer demand patterns.

Promote top-selling books more aggressively.


# 📍 Market & Customer Insights

📈 We've identified 10 countries with more consumers — focus marketing and supply in these regions to create potential loyal customers.

🌎 Explored data of diverse customers — analyze the genres they prefer and recommend similar books to increase engagement.

💰 We have a list of top revenue-generating customers — provide exclusive offers or personalized messages to maintain their interest.

# 📚 Conclusion

🔍 Monitor popular genres based on order history to ensure you're offering what readers love.

1. This project analyzed 500+ rows of data from Books, Orders, and Customers tables.


2. We discovered a rising customer base year by year, with 2023 having the highest engagement.


3. Fiction and Science Fiction genres emerged as the most borrowed, with changing trends over the years.


4. Revenue insights showed which books and customers contributed most to sales.


5. Monthly trends helped understand demand cycles and seasonality in orders.


6. Stock analysis classified books into understocked, overstocked, and optimum levels.


7. Customer segmentation revealed patterns of premium, regular, and low spenders.


8. Repeated and diverse readers were identified, aiding in customer retention strategies.


9. Time-based comparisons gave visibility into 2023 vs. 2024 borrowing patterns.


10. Overall, the project delivered actionable insights for inventory planning and customer targeting.


## Author

# SHAHISTA SHAIKH
# Contact me:
shaikhshahi326@gmail.com

