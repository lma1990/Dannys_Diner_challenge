# Dannys_Diner_challenge
The 1st Case Study- 8-week course from Danny Mia
## Introduction
Danny seriously loves Japanese food so in the beginning of 2021, he decides to embark upon a risky venture and opens up a cute little restaurant that sells his 3 favourite foods: sushi, curry and ramen.

Danny’s Diner is in need of your assistance to help the restaurant stay afloat - the restaurant has captured some very basic data from their few months of operation but have no idea how to use their data to help them run the business.

## Problem Statement
Danny wants to use the data to answer a few simple questions about his customers, especially about their visiting patterns, how much money they’ve spent and also which menu items are their favourite. Having this deeper connection with his customers will help him deliver a better and more personalised experience for his loyal customers.

He plans on using these insights to help him decide whether he should expand the existing customer loyalty program - additionally he needs help to generate some basic datasets so his team can easily inspect the data without needing to use SQL.

Danny has provided you with a sample of his overall customer data due to privacy issues - but he hopes that these examples are enough for you to write fully functioning SQL queries to help him answer his questions!

# Case Study Questions

What is the total amount each customer spent at the restaurant?
```
SELECT
    sales.price,
    sales.customer_id,
    menu.price
FROM dannys_diner.menu
JOIN
	product_id ON sale.product_id = menu.product_id
Group by
	customer_id
ORDER BY 
	customer_id
```

How many days has each customer visited the restaurant?
```
SELECT
	customer_id,
    COUNT(DISTINCT order_date) AS visits
FROM dannys_diner.sales
GROUP BY
    customer_id
```

**What was the first item from the menu purchased by each customer?**

```
WITH ordered_sales AS (
  SELECT
    sales.customer_id,
    RANK() OVER (
      PARTITION BY sales.customer_id
      ORDER BY sales.order_date
    ) AS order_rank,
    menu.product_name
  FROM dannys_diner.sales
  INNER JOIN dannys_diner.menu
    on sales.product_id = menu.product_id
)

SELECT DISTINCT
  customer_id,
  product_name
FROM ordered_sales
-- what about this?
WHERE order_rank = 1;

```
What is the most purchased item on the menu and how many times was it purchased by all customers?

```
SELECT
	product_id,
	COUNT(customer_id) AS TIMES_ORDERED
FROM
	dannys_diner.sales
GROUP BY
	product_id
ORDER BY
	product_id
DESC
```
Which item was the most popular for each customer?

```


Which item was purchased first by the customer after they became a member?
Which item was purchased just before the customer became a member?
What is the total items and amount spent for each member before they became a member?
If each $1 spent equates to 10 points and sushi has a 2x points multiplier - how many points would each customer have?
In the first week after a customer joins the program (including their join date) they earn 2x points on all items, not just sushi - how many points do customer A and B have at the end of January?



