# DAY 19 — SQL: JOIN + GROUP BY

## Topics Covered
- Aggregate functions after JOIN
- GROUP BY with JOIN
- Calculating revenue
- Revenue by product
- Revenue by category
- Revenue by customer
- Revenue by region
- Avoiding double-counting

---

## 1. Introduction

JOIN combines related tables, while GROUP BY groups records for calculations.

Together, they help answer business questions such as:
- Which product generates the highest revenue?
- Which category generates the most revenue?
- Which customer spends the most?
- Which region performs best?

## 2. Sample Dataset

### Products Table

| ProductID | ProductName | Category |
|---|---|---|
| 101 | Laptop | Electronics |
| 102 | Mouse | Electronics |
| 103 | Chair | Furniture |
| 104 | Desk | Furniture |

### Orders Table

| OrderID | ProductID | Customer | Region | Quantity | Price |
|---|---|---|---|---:|---:|
| 1 | 101 | Akash | South | 2 | 40000 |
| 2 | 102 | Priya | North | 5 | 500 |
| 3 | 103 | Akash | South | 3 | 3000 |
| 4 | 101 | Rahul | East | 1 | 40000 |
| 5 | 104 | Priya | North | 2 | 7000 |
| 6 | 102 | Akash | South | 4 | 500 |

## 3. Calculating Revenue

Revenue is calculated using:

**Revenue = Quantity × Price**

```sql
SELECT
    Quantity * Price AS Revenue
FROM Orders;
```

This calculates revenue for each order record.

## 4. Revenue by Product

```sql
SELECT
    Products.ProductName,
    SUM(Orders.Quantity * Orders.Price) AS Revenue
FROM Orders
INNER JOIN Products
ON Orders.ProductID = Products.ProductID
GROUP BY Products.ProductName;
```

### Expected Output

| ProductName | Revenue |
|---|---:|
| Laptop | 120000 |
| Mouse | 4500 |
| Chair | 9000 |
| Desk | 14000 |

## 5. Revenue by Category

```sql
SELECT
    Products.Category,
    SUM(Orders.Quantity * Orders.Price) AS Revenue
FROM Orders
INNER JOIN Products
ON Orders.ProductID = Products.ProductID
GROUP BY Products.Category;
```

### Expected Output

| Category | Revenue |
|---|---:|
| Electronics | 124500 |
| Furniture | 23000 |

Electronics generates the highest revenue in this dataset.

## 6. Revenue by Customer

```sql
SELECT
    Customer,
    SUM(Quantity * Price) AS Revenue
FROM Orders
GROUP BY Customer;
```

### Expected Output

| Customer | Revenue |
|---|---:|
| Akash | 89000 |
| Priya | 16500 |
| Rahul | 40000 |

## 7. Revenue by Region

```sql
SELECT
    Region,
    SUM(Quantity * Price) AS Revenue
FROM Orders
GROUP BY Region;
```

### Expected Output

| Region | Revenue |
|---|---:|
| South | 89000 |
| North | 16500 |
| East | 40000 |

## 8. Find the Product with the Highest Revenue

```sql
SELECT
    Products.ProductName,
    SUM(Orders.Quantity * Orders.Price) AS Revenue
FROM Orders
INNER JOIN Products
ON Orders.ProductID = Products.ProductID
GROUP BY Products.ProductName
ORDER BY Revenue DESC
LIMIT 1;
```

### Expected Output

| ProductName | Revenue |
|---|---:|
| Laptop | 120000 |

## 9. Understanding Double-Counting

Double-counting means counting the same value more than once.

When joining tables, one row from a table may match multiple rows in another table. This can duplicate values and produce incorrect totals.

### Example

Orders:

| OrderID | OrderTotal |
|---|---:|
| 1 | 1000 |
| 2 | 2000 |

OrderDetails:

| OrderID | Product |
|---|---|
| 1 | Laptop |
| 1 | Mouse |
| 2 | Keyboard |

After joining, Order 1's total of 1000 appears twice.

Incorrect total:

1000 + 1000 + 2000 = 4000

Correct total:

1000 + 2000 = 3000

### How to Avoid Double-Counting

- Understand what one row represents in each table.
- Check whether JOIN creates duplicate records.
- Calculate revenue at the correct level of detail.
- Aggregate data before joining when necessary.
- Avoid blindly summing repeated order-level values.

## 10. Aggregate Before Joining

```sql
SELECT
    OrderID,
    SUM(Quantity * UnitPrice) AS OrderRevenue
FROM OrderDetails
GROUP BY OrderID;
```

This calculates revenue for each order before joining it with another table.

## 11. SQL Practice Questions

### Q1.
Calculate revenue by product.

### Q2.
Calculate revenue by category.

### Q3.
Calculate revenue by customer.

### Q4.
Calculate revenue by region.

### Q5.
Find the product with the highest revenue.

### Q6.
Explain double-counting after a JOIN.

## 12. Practice Solutions

### Solution 1 — Revenue by Product

```sql
SELECT
    Products.ProductName,
    SUM(Orders.Quantity * Orders.Price) AS Revenue
FROM Orders
INNER JOIN Products
ON Orders.ProductID = Products.ProductID
GROUP BY Products.ProductName;
```

### Solution 2 — Revenue by Category

```sql
SELECT
    Products.Category,
    SUM(Orders.Quantity * Orders.Price) AS Revenue
FROM Orders
INNER JOIN Products
ON Orders.ProductID = Products.ProductID
GROUP BY Products.Category;
```

### Solution 3 — Revenue by Customer

```sql
SELECT
    Customer,
    SUM(Quantity * Price) AS Revenue
FROM Orders
GROUP BY Customer;
```

### Solution 4 — Revenue by Region

```sql
SELECT
    Region,
    SUM(Quantity * Price) AS Revenue
FROM Orders
GROUP BY Region;
```

### Solution 5 — Highest Revenue Product

```sql
SELECT
    Products.ProductName,
    SUM(Orders.Quantity * Orders.Price) AS Revenue
FROM Orders
INNER JOIN Products
ON Orders.ProductID = Products.ProductID
GROUP BY Products.ProductName
ORDER BY Revenue DESC
LIMIT 1;
```

**Expected Output:** Laptop — 120000

### Solution 6 — Double-Counting

Double-counting means counting the same value more than once, usually because a JOIN duplicates records. It can result in incorrect totals and misleading analysis.

---

## 13. Key Takeaways

- JOIN combines related tables.
- GROUP BY groups records.
- SUM() calculates total revenue.
- Revenue = Quantity × Price.
- Revenue can be calculated by product, category, customer and region.
- Double-counting can cause incorrect business insights.
- Understanding the grain of a dataset is important before joining and aggregating.

## Day 19 Completion

- [x] Learned JOIN + GROUP BY.
- [x] Calculated revenue by product.
- [x] Calculated revenue by category.
- [x] Calculated revenue by customer.
- [x] Calculated revenue by region.
- [x] Understood double-counting.
- [x] Practised SQL queries.

**Day 19 — SQL Learning Completed!**
