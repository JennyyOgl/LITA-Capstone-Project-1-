# LITA-Capstone-Project-1-
Project 1 of the Capstone project

```SQL
select * from Capstone_SalesData
```
```SQL
select count(distinct customer_id) as number_of_clients
from Capstone_SalesData
```

```SQL
ALTER TABLE Capstone_SalesData
alter COLUMN unitprice DECIMAL(11, 2)
```

> retrieve the total sales for each product category

```SQL
select product, sum(quantity) sales
from Capstone_SalesData
group by product
```

> find the number of sales transactions in each region

```SQL
select count(orderID) as orders, region
from Capstone_SalesData
group by region
```

> find the highest-selling product by total sales value.

```SQL
select product from 
(select product, sum(quantity) sales
from Capstone_SalesData
group by product) as table2
where sales=80000
```

> calculate total revenue per product

```SQL
select orderID, sum(unitprice*quantity) as order_price
from Capstone_SalesData
group by orderID
```

> calculate monthly sales totals for the current year 

```SQL
select sum(unitprice*quantity) as order_price, datepart(MONTH, OrderDate) as purchase_month
from Capstone_SalesData
where datepart(YEAR, OrderDate) = 2024
group by datepart(MONTH, OrderDate)
```

> find the top 5 customers by total purchase amount 
 
 ```SQL
create view purchase_clients as
(select customer_id, sum(unitprice*quantity) as order_price
from Capstone_SalesData
group by customer_id)
```

```SQL
select top 5* from purchase_clients
order by order_price desc
```

> identify products with no sales in the last quarter

```SQL
select distinct product from Capstone_SalesData
where product not in
(select product
from Capstone_SalesData
where datepart(MONTH, OrderDate) > 6
and datepart(MONTH, OrderDate) < 11
and datepart(YEAR, OrderDate) = 2024) 
```
 
