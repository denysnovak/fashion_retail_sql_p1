# Fashion Retail Sales Analysis (SQL Project)

## Project Goal
Analyze customer purchases and review ratings from a fashion retail dataset to uncover insights such as top-rated items, payment trends, and daily sales performance.

## Tools Used
- SQL (aggregation, filtering, grouping, HAVING, CASE statements)
- Any SQL engine (PostgreSQL, MySQL, SQLite, etc.)

## Dataset
- `cleaned_fashion_retail_sales`
- Contains information about purchases, review ratings, payment method, and purchase dates.

## How to Run
1. Load the dataset into your SQL engine  
2. Execute the provided SQL scripts / queries  

## SQL Code:

```sql

## Question 1: Count total purchases in the dataset

select count(`Item Purchased`)
from cleaned_fashion_retail_sales; 

## Question 2: Count unique customers 

select distinct (`Customer Reference ID`)
from cleaned_fashion_retail_sales;

## Question 3: Find the most expensive item purchased 

select `Item Purchased`, `Purchase Amount (USD)`
from cleaned_fashion_retail_sales
order by `Purchase Amount (USD)` desc
limit 1;

## Question 4: Display first 10 records with Customer Reference ID, Item Purchased, Purchase Amount 

select `Customer Reference ID`, `Item Purchased`, `Purchase Amount (USD)`
from cleaned_fashion_retail_sales
limit 10;

## Question 5: Calculate the average Review Rating across all purchases

select round(avg(`Review Rating`),2) as avg_rating
from cleaned_fashion_retail_sales;

## Question 6: Count purchases by Payment Method

select count(`Customer Reference ID`), `Payment Method`
from cleaned_fashion_retail_sales
group by `Payment Method` ;

## Question 7: Identify the customer who spent the most money in total

select distinct `Customer Reference ID`, sum(`Purchase Amount (USD)`)
from cleaned_fashion_retail_sales
group by `Customer Reference ID` 
order by sum(`Purchase Amount (USD)`) desc
limit 1;

## Question 8: Find the most frequently purchased item

select `Item Purchased`, count(*) as purchase_count
from cleaned_fashion_retail_sales
group by `Item Purchased`
order by purchase_count desc
limit 1;

## Question 9: Calculate the average Purchase Amount (USD) for each Item Purchased

select `Item Purchased`, round(avg(`Purchase Amount (USD)`), 2) as avg_price
from cleaned_fashion_retail_sales
group by 1;

## Question 10: Count number of purchases for each Date Purchase

select `Date Purchase`, count(`Item Purchased`) as purchase_for_each_date
from cleaned_fashion_retail_sales
group by `Date Purchase`;

## Question 11: Find customers who left more than 4-star rating but purchased less than 3 items in total

select `Customer Reference ID`, count(*) as total_purchases
from cleaned_fashion_retail_sales
where `Review Rating` >4
group by `Customer Reference ID`
having total_purchases <3;


## Question 12: Find the top 5 items with the highest average Review Rating, with at least 10 purchases

select `Item Purchased`, avg(`Review Rating`) as avg_rating, count(*) as purchase_count
from cleaned_fashion_retail_sales
group by `Item Purchased`
having count(*) >= 10
order by avg_rating desc
limit 5;

## Question 13: Calculate the percentage of purchases paid with Credit Card

select 
(sum(case
when `Payment Method`= 'Credit Card' then 1 
else 0 end) * 100) / count(*) as percent_card_payments
from cleaned_fashion_retail_sales;

## Question 14: Identify customers who purchased the same item more than once, showing Customer Reference ID and Item Purchased

select `Customer Reference ID`, `Item Purchased`
from cleaned_fashion_retail_sales
group by `Customer Reference ID`, `Item Purchased`
having count(`Item Purchased`) > 1;

## Question 15: For each date, calculate total revenue, average rating, and number of purchases

select `Date Purchase`, sum(`Purchase Amount (USD)`) as total_revenue , round(avg(`Review Rating`),2) as avg_rating, count(*) as purchases_number
from cleaned_fashion_retail_sales
group by `Date Purchase`;
