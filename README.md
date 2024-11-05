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
  
select SUM(productsale) as Shoes_Sales from [dbo].[Sales Data 1]
where Product = 'Shoes'

This query is used individually for all the products 





![Screenshot 2024-11-05 111204](https://github.com/user-attachments/assets/4d181f46-4f61-4dc1-93f1-2b8eae01e7e4)

- find the number of sales transactions in each region.

select region,
count (*) AS Sales from [dbo].[Sales Data 1]
group by region


![Screenshot 2024-11-05 110442](https://github.com/user-attachments/assets/d1cfbe31-a44f-4ebb-bd70-19cf2895a6ae)


- find the highest-selling product by total sales value.
  
select TOP 1 product,
SUM (PRODUCTSALE) AS HIGHESTSELLING from [dbo].[Sales Data 1]
group by product
order by 2 desc

![Screenshot 2024-11-05 110721](https://github.com/user-attachments/assets/04f80f15-8dab-42c0-8f46-7f0520405331)


- calculate total revenue per product.
  
select PRODUCT, SUM(productsale) as totalsales from [dbo].[Sales Data 1]
GROUP BY PRODUCT


![Screenshot 2024-11-05 111303](https://github.com/user-attachments/assets/d00d2839-f9f6-40ad-a8e0-6e58436bb551)

- calculate monthly sales totals for the current year.
  
select months, 
SUM (PRODUCTSALE) AS sales from [dbo].[Sales Data 1]
where year = '2024'
group by months;

![Screenshot 2024-11-05 111439](https://github.com/user-attachments/assets/e3389cb8-cdd9-434e-9ddc-60668a6cc5b2)



- find the top 5 customers by total purchase amount.
select top 5 [Customer_Id] as Customerid,
SUM (productsale) as top5 from [dbo].[Sales Data 1] 
group by [Customer_Id] 
order by 2 desc



![Screenshot 2024-11-05 111457](https://github.com/user-attachments/assets/16c19d2a-4fc4-4606-a31c-d43f70197188)


- calculate the percentage of total sales contributed by each region.


- identify products with no sales in the last quarter

select product from [dbo].[Sales Data 1]
group by product 
having sum(case 
when  [OrderDate] between '2024-06-01' and '2024-08-31'
then 1 else 0
End) = 0

![Screenshot 2024-11-05 111527](https://github.com/user-attachments/assets/3aaff5ab-70f8-44f1-8fe8-01a4344b5fb0)



##### Using PowerBI




![Screenshot 2024-11-05 111624](https://github.com/user-attachments/assets/9877ee8c-25bd-4f83-9e97-6e841280bfc2)



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

![Screenshot 2024-11-05 121638](https://github.com/user-attachments/assets/9a441c32-a3a8-4ac7-8d7b-63b51dc8ee19)

- find the most popular subscription type by the number of customers.
select [SubscriptionType],
count (*) as noofcustomers from [dbo].[Customer Data]
group by subscriptiontype

![Screenshot 2024-11-05 124036](https://github.com/user-attachments/assets/e3268429-2850-42ab-b08b-1c88d870bebf)


- find customers who canceled their subscription within 6 months.
select [CustomerID], [SubscriptionStart], [SubscriptionEnd],
DATEDIFF(month, [SubscriptionStart], [SubscriptionEnd])
as duration from [dbo].[Customer Data]
where [Canceled] = 'true' and datediff(month, [SubscriptionStart], [SubscriptionEnd])<=6


![Screenshot 2024-11-05 124054](https://github.com/user-attachments/assets/04f6ce62-20ea-46a0-81db-b06f2d257eab)

- Calculate the average subscription duration for all customers.
select AVG((DATEDIFF(month,[SubscriptionStart],[SubscriptionEnd] )
)) as'avgdur' from [dbo].[Customer Data]

 ![Screenshot 2024-11-05 124113](https://github.com/user-attachments/assets/235590f6-1108-4d6b-8df5-3562a8f87278)
  
- find customers with subscriptions longer than 12 months.
select [CustomerID], [SubscriptionStart], [SubscriptionEnd],
DATEDIFF(month, [SubscriptionStart], [SubscriptionEnd])
as duration from [dbo].[Customer Data]
where datediff(month, [SubscriptionStart], [SubscriptionEnd])>12

![Screenshot 2024-11-05 124141](https://github.com/user-attachments/assets/ce7fb811-9982-4b5c-b015-2395d6bc999b)

- calculate total revenue by subscription type.
select Sum ([Revenue]) as totalrev from [dbo].[Customer Data]
where ([SubscriptionType]) = 'Basic' or
([SubscriptionType]) = 'premium' or
([SubscriptionType]) = 'standard' 
group by [SubscriptionType]

![Screenshot 2024-11-05 124527](https://github.com/user-attachments/assets/58d5a0bc-fc56-4176-b253-655fe089dd03)

- find the top 3 regions by subscription cancellations.
select top 3 Region, COUNT (Canceled) AS CANCELED from [dbo].[Customer Data] 
  group by [Region]

  ![Screenshot 2024-11-05 124600](https://github.com/user-attachments/assets/82356fca-ae1f-419b-ab43-6d5466f554cf)
  

- find the total number of active and canceled subscriptions.

select Canceled, Count(Canceled) as active from [dbo].[Customer Data] 
WHERE [Canceled] = 'false'
group by [Canceled]

select Canceled, Count(Canceled) as false from [dbo].[Customer Data] 
WHERE [Canceled] = 'true'
group by [Canceled]

![Screenshot 2024-11-05 124720](https://github.com/user-attachments/assets/dd59d627-f589-464a-929d-7e6fe79d6181)



#### Using PowerBI




 ![Screenshot 2024-11-05 121936](https://github.com/user-attachments/assets/d86f0290-375e-43a3-81dd-bfe268800d9d)


