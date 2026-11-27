# DAY 21 — SQL: JOIN CHECKPOINT

## Topics Covered

- INNER JOIN revision
- LEFT JOIN revision
- Multi-table JOIN
- Aggregate functions
- JOIN with GROUP BY
- Understanding NULL values
- Avoiding double-counting
- Mini relational-data test

---

## 1. Introduction

SQL JOINs are used to combine data from multiple related tables.

In data analytics, information is often stored in separate tables. JOIN helps us connect that information and generate meaningful business insights.

For example:
- Find customer orders.
- Calculate total sales per customer.
- Identify customers who have not placed orders.
- Calculate revenue by product or category.

## 2. Sample Datasets

### Customers Table

| customer_id | name |
|---|---|
| 1 | Akash |
| 2 | Ravi |
| 3 | Priya |

### Orders Table

| order_id | customer_id | amount |
|---|---|---:|
| 101 | 1 | 500 |
| 102 | 1 | 300 |
| 103 | 2 | 700 |

## 3. INNER JOIN

INNER JOIN returns only records that have matching values in both tables.

### Syntax

```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.common_column = table2.common_column;
```

### Example

```sql
SELECT Customers.name, Orders.amount
FROM Customers
INNER JOIN Orders
ON Customers.customer_id = Orders.customer_id;
```

### Expected Output

| name | amount |
|---|---:|
| Akash | 500 |
| Akash | 300 |
| Ravi | 700 |

**Explanation:** Priya is not included because she does not have a matching order.

## 4. LEFT JOIN

LEFT JOIN returns all records from the left table and matching records from the right table.

If no matching record exists, SQL returns NULL for the right-table columns.

### Example

```sql
SELECT Customers.name, Orders.amount
FROM Customers
LEFT JOIN Orders
ON Customers.customer_id = Orders.customer_id;
```

### Expected Output

| name | amount |
|---|---:|
| Akash | 500 |
| Akash | 300 |
| Ravi | 700 |
| Priya | NULL |

**Explanation:** Priya appears because LEFT JOIN preserves all records from the Customers table.

## 5. Multi-table JOIN

Multi-table JOIN combines information from three or more related tables.

### Products Table

| product_id | product_name |
|---|---|
| 10 | Laptop |
| 20 | Mouse |

### OrderDetails Table

| order_id | product_id | quantity |
|---|---|---:|
| 101 | 10 | 2 |
| 102 | 20 | 3 |
| 103 | 10 | 1 |

### Example

```sql
SELECT
    Orders.order_id,
    Customers.name,
    Products.product_name,
    OrderDetails.quantity
FROM Orders
INNER JOIN Customers
ON Orders.customer_id = Customers.customer_id
INNER JOIN OrderDetails
ON Orders.order_id = OrderDetails.order_id
INNER JOIN Products
ON OrderDetails.product_id = Products.product_id;
```

**Explanation:**

- First JOIN connects Orders with Customers.
- Second JOIN connects Orders with OrderDetails.
- Third JOIN connects OrderDetails with Products.

This helps us understand which customer purchased which product.

## 6. Aggregate Functions

Aggregate functions perform calculations on multiple records.

| Function | Purpose |
|---|---|
| SUM() | Calculates total |
| COUNT() | Counts records |
| AVG() | Calculates average |
| MIN() | Finds minimum value |
| MAX() | Finds maximum value |

### Example

```sql
SELECT SUM(amount) AS total_sales
FROM Orders;
```

Expected output:

| total_sales |
|---:|
| 1500 |

## 7. JOIN with GROUP BY

GROUP BY groups records with the same value so aggregate functions can calculate results for each group.

### Example: Total Sales by Customer

```sql
SELECT
    Customers.name,
    SUM(Orders.amount) AS total_sales
FROM Customers
INNER JOIN Orders
ON Customers.customer_id = Orders.customer_id
GROUP BY Customers.name;
```

### Expected Output

| name | total_sales |
|---|---:|
| Akash | 800 |
| Ravi | 700 |

## 8. Understanding Double-Counting

Double-counting happens when the same value is counted more than once because of duplicated rows created by JOIN operations.

Example:

Suppose a customer has two orders worth ₹500 and ₹300.

After joining the customer table with the orders table, the customer's information appears twice.

This is normal for a one-to-many relationship.

However, if we join another table with multiple matching records, rows can multiply further.

**How to avoid double-counting:**

- Understand table relationships before joining.
- Check the number of rows after each JOIN.
- Aggregate at the correct level.
- Avoid using DISTINCT as a blind fix.
- Pre-aggregate data when necessary.

## 9. Mini Relational-Data Test

1. Which JOIN returns only matching records?
2. Which JOIN preserves every row from the left table?
3. Which function calculates total sales?
4. Which clause groups similar records?
5. Akash has orders worth ₹500 and ₹300. What is his total sales?
6. What does SQL return for unmatched right-table columns in a LEFT JOIN?

### Solutions

1. INNER JOIN
2. LEFT JOIN
3. SUM()
4. GROUP BY
5. ₹800
6. NULL

## 10. Key Takeaways

- INNER JOIN retrieves matching records.
- LEFT JOIN preserves all left-table records.
- Multi-table JOIN connects multiple related tables.
- Aggregate functions perform calculations.
- GROUP BY groups records for analysis.
- Understanding relationships helps prevent double-counting.

## Completion Checklist

- [ ] Revised INNER JOIN
- [ ] Revised LEFT JOIN
- [ ] Practised multi-table JOIN
- [ ] Revised aggregate functions
- [ ] Practised JOIN with GROUP BY
- [ ] Understood double-counting
- [ ] Completed SQL mini test

**Day 21 SQL Checkpoint — Completed / In Progress**
