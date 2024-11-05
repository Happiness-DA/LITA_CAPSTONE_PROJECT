# LITA_CAPSTONE_PROJECT

### Project 1: Sales Performance Analysis for a Retail Store
#### Project Overview
In this project, you are tasked with analyzing the sales performance of a retail store.
You will need to explore sales data to uncover key insights such as top-selling products, regional
performance, and monthly sales trends. The goal is to produce an interactive Power BI
dashboard that highlights these findings.

 ##### Using Excel: 
 Use pivot tables to summarize total sales by product, region, and month.
 Create column "totalsales" = quantity * unitprice 
 Insert > pivot table > product, product sales. 
 This is done for every parameter to create the pivot table.

 Calculating Average sales per product and total revenue by region 
 Use excel function Averageif where range = product column , Criteria = product, average range = total sales column
 Use excel function sumif where range = region column, criteria = region, sumrange = total sales column

##### Using SQL:
- retrieve the total sales for each product category.
  
select SUM(productsale) as Shirt_Sales from [dbo].[Sales Data 1]
where Product = 'Shirt'
This query is used individually for all the products 

- find the number of sales transactions in each region.

select region,
count (*) AS Sales from [dbo].[Sales Data 1]
group by region

- find the highest-selling product by total sales value.
  
select product,
SUM (PRODUCTSALE) AS totalsales from [dbo].[Sales Data 1]
group by product
order by 2 desc

- calculate total revenue per product.
  
select SUM(productsale) as Shoes_Sales from [dbo].[Sales Data 1]
where Product = 'Shoes'

- calculate monthly sales totals for the current year.
  
select months, 
SUM (PRODUCTSALE) AS sales from [dbo].[Sales Data 1]
where year = '2024'
group by months;




- find the top 5 customers by total purchase amount.
select top 5 [Customer_Id] as Customerid,
SUM (productsale) as top5 from [dbo].[Sales Data 1] 
group by [Customer_Id] 
order by 2 desc

- calculate the percentage of total sales contributed by each region.
- identify products with no sales in the last quarter



##### Using PowerBI




### Project 2: Customer Segmentation for a Subscription Service
#### Project Overview
 This project involves analyzing customer data for a subscription service to identify
segments and trends. Your goal is to understand customer behavior, track subscription types,
and identify key trends in cancellations and renewals. The final deliverable is a Power BI
dashboard that presents your analysis.

 ##### Using Excel 
 Calculate the average subscription duration and identify the most popular
subscription types.
Use excel function AVERAGE(I2,I75001) 
Use excel function Countif(region column, region)

##### Using SQL
- retrieve the total number of customers from each region.
select region,
count (*) AS Customername from [dbo].[Customer Data]
group by region 

- find the most popular subscription type by the number of customers.
select [SubscriptionType],
count (*) as noofcustomers from [dbo].[Customer Data]
group by subscriptiontype 

- find customers who canceled their subscription within 6 months.
select [CustomerID], [SubscriptionStart], [SubscriptionEnd],
DATEDIFF(month, [SubscriptionStart], [SubscriptionEnd])
as duration from [dbo].[Customer Data]
where [Canceled] = 'true' and datediff(month, [SubscriptionStart], [SubscriptionEnd])<=6

- Calculate the average subscription duration for all customers.
select AVG((DATEDIFF(month,[SubscriptionStart],[SubscriptionEnd] )
)) as'avgdur' from [dbo].[Customer Data]
  
- find customers with subscriptions longer than 12 months.
select [CustomerID], [SubscriptionStart], [SubscriptionEnd],
DATEDIFF(month, [SubscriptionStart], [SubscriptionEnd])
as duration from [dbo].[Customer Data]
where datediff(month, [SubscriptionStart], [SubscriptionEnd])>12

- calculate total revenue by subscription type.
select Sum ([Revenue]) as totalrev from [dbo].[Customer Data]
where ([SubscriptionType]) = 'Basic' or
([SubscriptionType]) = 'premium' or
([SubscriptionType]) = 'standard' 
group by [SubscriptionType]

- find the top 3 regions by subscription cancellations.
- find the total number of active and canceled subscriptions.



 

