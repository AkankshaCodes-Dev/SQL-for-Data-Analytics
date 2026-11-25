# DAY 20 — SQL: JOIN + CASE + HAVING

## Topics Covered

- Combining multiple tables using JOIN
- Using CASE statements
- Creating categories based on conditions
- Aggregate functions with JOIN
- GROUP BY with CASE
- HAVING to filter grouped results
- Solving business questions using multiple tables

---

## 1. Introduction

SQL JOIN, CASE and HAVING are important concepts used in business data analysis.

- JOIN combines related data from multiple tables.
- CASE creates categories based on conditions.
- GROUP BY groups similar records for calculations.
- HAVING filters grouped results.

Together, these concepts help answer business questions such as:

- Which customers spend the most?
- Which orders belong to the High, Medium or Low category?
- How many orders are placed by each customer?
- Which customers have total spending above ₹1,000?
- Which product categories generate higher sales?

## 2. Sample Dataset

### Customers Table

| CustomerID | CustomerName | City |
|---|---|---|
| 1 | Akash | Hyderabad |
| 2 | Priya | Bangalore |
| 3 | Rahul | Mumbai |

### Products Table

| ProductID | ProductName | Category |
|---|---|---|
| 101 | Laptop | Electronics |
| 102 | Mouse | Electronics |
| 103 | Chair | Furniture |

### Orders Table

| OrderID | CustomerID | ProductID | Quantity | Price |
|---|---|---|---|---|
| 1 | 1 | 101 | 1 | 40000 |
| 2 | 2 | 102 | 2 | 500 |
| 3 | 1 | 103 | 1 | 3000 |
| 4 | 3 | 101 | 1 | 40000 |
| 5 | 2 | 103 | 2 | 3000 |
| 6 | 1 | 102 | 2 | 500 |

## 3. Understanding JOIN

JOIN combines records from two or more tables using a related column.

### Example: Display Customer Names and Order Amounts

```sql
SELECT
    Customers.CustomerName,
    Orders.OrderID,
    Orders.Quantity * Orders.Price AS OrderAmount
FROM Customers
INNER JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

### Expected Output

| CustomerName | OrderID | OrderAmount |
|---|---|---|
| Akash | 1 | 40000 |
| Priya | 2 | 1000 |
| Akash | 3 | 3000 |
| Rahul | 4 | 40000 |
| Priya | 5 | 6000 |
| Akash | 6 | 1000 |

JOIN connects customers with their corresponding orders.

## 4. Understanding CASE Statement

CASE is used to create categories based on specified conditions.

It works similarly to IF-ELSE statements in Python.

### Syntax

```sql
CASE
    WHEN condition THEN result
    WHEN condition THEN result
    ELSE result
END
```

### Example: Categorize Orders

Business requirement:

- Amount >= 1500 → High
- Amount >= 800 → Medium
- Otherwise → Low

```sql
SELECT
    OrderID,
    Quantity * Price AS OrderAmount,
    CASE
        WHEN Quantity * Price >= 1500 THEN 'High'
        WHEN Quantity * Price >= 800 THEN 'Medium'
        ELSE 'Low'
    END AS OrderCategory
FROM Orders;
```

### Expected Output

| OrderID | OrderAmount | OrderCategory |
|---|---|---|
| 1 | 40000 | High |
| 2 | 1000 | Medium |
| 3 | 3000 | High |
| 4 | 40000 | High |
| 5 | 6000 | High |
| 6 | 1000 | Medium |

CASE checks conditions from top to bottom and returns the first matching result.

## 5. Using JOIN with CASE

We can combine JOIN and CASE to categorize customer orders.

### Example: Display Customer Names and Order Categories

```sql
SELECT
    Customers.CustomerName,
    Orders.OrderID,
    Orders.Quantity * Orders.Price AS OrderAmount,
    CASE
        WHEN Orders.Quantity * Orders.Price >= 1500
        THEN 'High'
        ELSE 'Low'
    END AS OrderCategory
FROM Customers
INNER JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

This query combines customer information with order details and classifies each order.

## 6. Understanding GROUP BY with JOIN

GROUP BY groups records with the same value.

It is commonly used with aggregate functions such as:

- SUM()
- COUNT()
- AVG()
- MAX()
- MIN()

### Example: Find Total Spending by Each Customer

```sql
SELECT
    Customers.CustomerName,
    SUM(Orders.Quantity * Orders.Price) AS TotalSpending
FROM Customers
INNER JOIN Orders
ON Customers.CustomerID = Orders.CustomerID
GROUP BY Customers.CustomerName;
```

### Expected Output

| CustomerName | TotalSpending |
|---|---|
| Akash | 44000 |
| Priya | 7000 |
| Rahul | 40000 |

GROUP BY combines each customer's orders and SUM calculates their total spending.

## 7. Understanding HAVING

HAVING is used to filter grouped results.

It is commonly used with aggregate functions.

### Example: Find Customers Spending More Than ₹10,000

```sql
SELECT
    Customers.CustomerName,
    SUM(Orders.Quantity * Orders.Price) AS TotalSpending
FROM Customers
INNER JOIN Orders
ON Customers.CustomerID = Orders.CustomerID
GROUP BY Customers.CustomerName
HAVING SUM(Orders.Quantity * Orders.Price) > 10000;
```

### Expected Output

| CustomerName | TotalSpending |
|---|---|
| Akash | 44000 |
| Rahul | 40000 |

Only customers whose total spending exceeds ₹10,000 are displayed.

## 8. Difference Between WHERE and HAVING

| WHERE | HAVING |
|---|---|
| Filters individual rows | Filters grouped results |
| Used before GROUP BY | Used after GROUP BY |
| Filters normal column values | Commonly filters aggregate results |
| Example: Price > 500 | Example: SUM(Price) > 5000 |

### Example Using WHERE

```sql
SELECT *
FROM Orders
WHERE Price > 1000;
```

### Example Using HAVING

```sql
SELECT
    CustomerID,
    SUM(Quantity * Price) AS TotalSpending
FROM Orders
GROUP BY CustomerID
HAVING SUM(Quantity * Price) > 10000;
```

## 9. Combining JOIN + CASE + GROUP BY + HAVING

This is the most important combination of today's lesson.

### Business Question

Find customer-wise total spending, classify customers as Premium or Regular and display only customers whose total spending exceeds ₹10,000.

Business rules:

- Spending >= ₹15,000 → Premium
- Spending below ₹15,000 → Regular
- Display only customers spending above ₹10,000.

```sql
SELECT
    Customers.CustomerName,
    SUM(Orders.Quantity * Orders.Price) AS TotalSpending,

    CASE
        WHEN SUM(Orders.Quantity * Orders.Price) >= 15000
        THEN 'Premium'
        ELSE 'Regular'
    END AS CustomerCategory

FROM Customers

INNER JOIN Orders
ON Customers.CustomerID = Orders.CustomerID

GROUP BY
    Customers.CustomerID,
    Customers.CustomerName

HAVING SUM(Orders.Quantity * Orders.Price) > 10000;
```

### Expected Output

| CustomerName | TotalSpending | CustomerCategory |
|---|---|---|
| Akash | 44000 | Premium |
| Rahul | 40000 | Premium |

### Understanding the Query

1. FROM Customers — Select the customer table.
2. INNER JOIN Orders — Connect customer and order tables.
3. ON — Match customer IDs.
4. SUM() — Calculate total spending.
5. GROUP BY — Group records customer-wise.
6. CASE — Classify customers.
7. HAVING — Filter customers based on total spending.

## 10. Business Questions

### Q1.
Display customer names and their order amounts using JOIN.

### Q2.
Calculate total spending by each customer.

### Q3.
Find customers whose total spending exceeds ₹10,000.

### Q4.
Categorize orders as High, Medium or Low using CASE.

### Q5.
Find the number of orders placed by each customer.

### Q6.
Find customers who placed more than one order.

### Q7.
Calculate average order amount for each customer.

### Q8.
Display customers whose average order amount exceeds ₹5,000.

### Q9.
Classify customers as Premium or Regular based on total spending.

### Q10.
Display customer names, total spending and customer category, showing only customers spending above ₹10,000.

## 11. Practice Solutions

### Solution 1 — Customer Names and Order Amounts

```sql
SELECT
    Customers.CustomerName,
    Orders.OrderID,
    Orders.Quantity * Orders.Price AS OrderAmount
FROM Customers
INNER JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

### Solution 2 — Total Spending by Customer

```sql
SELECT
    Customers.CustomerName,
    SUM(Orders.Quantity * Orders.Price) AS TotalSpending
FROM Customers
INNER JOIN Orders
ON Customers.CustomerID = Orders.CustomerID
GROUP BY Customers.CustomerID, Customers.CustomerName;
```

### Solution 3 — Customers Spending Above ₹10,000

```sql
SELECT
    CustomerID,
    SUM(Quantity * Price) AS TotalSpending
FROM Orders
GROUP BY CustomerID
HAVING SUM(Quantity * Price) > 10000;
```

### Solution 4 — Order Classification

```sql
SELECT
    OrderID,
    Quantity * Price AS Amount,
    CASE
        WHEN Quantity * Price >= 1500 THEN 'High'
        WHEN Quantity * Price >= 800 THEN 'Medium'
        ELSE 'Low'
    END AS Category
FROM Orders;
```

### Solution 5 — Number of Orders by Customer

```sql
SELECT
    CustomerID,
    COUNT(OrderID) AS TotalOrders
FROM Orders
GROUP BY CustomerID;
```

### Solution 6 — Customers with More Than One Order

```sql
SELECT
    CustomerID,
    COUNT(OrderID) AS TotalOrders
FROM Orders
GROUP BY CustomerID
HAVING COUNT(OrderID) > 1;
```

### Solution 7 — Average Order Amount

```sql
SELECT
    CustomerID,
    AVG(Quantity * Price) AS AverageAmount
FROM Orders
GROUP BY CustomerID;
```

### Solution 8 — Average Order Amount Above ₹5,000

```sql
SELECT
    CustomerID,
    AVG(Quantity * Price) AS AverageAmount
FROM Orders
GROUP BY CustomerID
HAVING AVG(Quantity * Price) > 5000;
```

### Solution 9 — Premium and Regular Customers

```sql
SELECT
    CustomerID,
    SUM(Quantity * Price) AS TotalSpending,
    CASE
        WHEN SUM(Quantity * Price) >= 15000
        THEN 'Premium'
        ELSE 'Regular'
    END AS CustomerCategory
FROM Orders
GROUP BY CustomerID;
```

### Solution 10 — JOIN + CASE + HAVING

```sql
SELECT
    Customers.CustomerName,
    SUM(Orders.Quantity * Orders.Price) AS TotalSpending,
    CASE
        WHEN SUM(Orders.Quantity * Orders.Price) >= 15000
        THEN 'Premium'
        ELSE 'Regular'
    END AS CustomerCategory
FROM Customers
INNER JOIN Orders
ON Customers.CustomerID = Orders.CustomerID
GROUP BY Customers.CustomerID, Customers.CustomerName
HAVING SUM(Orders.Quantity * Orders.Price) > 10000;
```

## 12. Key Takeaways

- JOIN combines related tables.
- CASE creates categories using conditions.
- CASE works similarly to IF-ELSE.
- GROUP BY groups records for calculations.
- SUM() calculates total values.
- COUNT() counts records.
- AVG() calculates average values.
- HAVING filters grouped results.
- WHERE filters individual rows.
- Combining JOIN, CASE, GROUP BY and HAVING helps solve real-world business problems.

## Day 20 Completion

- [x] Learned JOIN with multiple tables.
- [x] Learned CASE statements.
- [x] Created conditional categories.
- [x] Practised GROUP BY with JOIN.
- [x] Learned HAVING.
- [x] Combined JOIN + CASE + GROUP BY + HAVING.
- [x] Practised 10 business questions.

**Day 20 — SQL Learning Completed!**
