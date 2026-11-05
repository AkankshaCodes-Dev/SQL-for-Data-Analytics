# Day 16 — SQL: INNER JOIN

## Topics Learned
- Introduction to INNER JOIN
- Understanding the ON keyword
- Joining Customers and Orders tables
- Using INNER JOIN with GROUP BY
- Calculating useful results using COUNT() and SUM()

## 1. What is INNER JOIN?

INNER JOIN is used to combine rows from two tables when they have matching values in the specified columns.

It returns only matching records from both tables.

## 2. Practice Dataset

### Customers Table

| CustomerID | CustomerName | City |
|---|---|---|
| 101 | Akash | Hyderabad |
| 102 | Priya | Bangalore |
| 103 | Rahul | Chennai |
| 104 | Sneha | Mumbai |

### Orders Table

| OrderID | CustomerID | Quantity |
|---|---|---|
| 501 | 101 | 2 |
| 502 | 102 | 1 |
| 503 | 101 | 3 |
| 504 | 103 | 1 |
| 505 | 105 | 2 |

## 3. INNER JOIN Syntax

```sql
SELECT column_names
FROM table1
INNER JOIN table2
ON table1.common_column = table2.common_column;
```

### Understanding the Keywords

- SELECT: Specifies the columns to retrieve.
- FROM: Specifies the first table.
- INNER JOIN: Combines matching records.
- ON: Specifies the matching condition.

## 4. Joining Customers and Orders

```sql
SELECT
    Customers.CustomerName,
    Orders.OrderID,
    Orders.Quantity
FROM Customers
INNER JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

### Expected Output

| CustomerName | OrderID | Quantity |
|---|---|---|
| Akash | 501 | 2 |
| Priya | 502 | 1 |
| Akash | 503 | 3 |
| Rahul | 504 | 1 |

**Observation:**
- Sneha is excluded because she has no matching order.
- OrderID 505 is excluded because CustomerID 105 does not exist in the Customers table.

## 5. INNER JOIN with COUNT()

Question: How many orders did each customer place?

```sql
SELECT
    Customers.CustomerName,
    COUNT(Orders.OrderID) AS Total_Orders
FROM Customers
INNER JOIN Orders
ON Customers.CustomerID = Orders.CustomerID
GROUP BY Customers.CustomerName;
```

### Expected Output

| CustomerName | Total_Orders |
|---|---|
| Akash | 2 |
| Priya | 1 |
| Rahul | 1 |

## 6. INNER JOIN with SUM()

Question: What is the total quantity ordered by each customer?

```sql
SELECT
    Customers.CustomerName,
    SUM(Orders.Quantity) AS Total_Quantity
FROM Customers
INNER JOIN Orders
ON Customers.CustomerID = Orders.CustomerID
GROUP BY Customers.CustomerName;
```

### Expected Output

| CustomerName | Total_Quantity |
|---|---|
| Akash | 5 |
| Priya | 1 |
| Rahul | 1 |

## 7. Practice Questions with Solutions

**Q1. Which column connects Customers and Orders?**

Answer: CustomerID.

**Q2. Which keyword specifies the matching condition?**

Answer: ON.

**Q3. Why is OrderID 505 excluded?**

Answer: CustomerID 105 has no matching record in the Customers table.

**Q4. How many orders did Akash place?**

Answer: 2 orders (501 and 503).

**Q5. What is Akash's total ordered quantity?**

Answer: 5 (2 + 3).

## 8. Key Takeaways

- INNER JOIN combines matching records from two tables.
- ON specifies the columns used for matching.
- GROUP BY groups records for calculations.
- COUNT() counts records.
- SUM() calculates the total of numeric values.

## What I Learned

Today, I learned how to combine customer and order information using INNER JOIN. I also practised calculating total orders and quantities using COUNT(), SUM() and GROUP BY.

**Day 16 — SQL Completed!**
