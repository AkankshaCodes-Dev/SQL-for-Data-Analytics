# DAY 17 — SQL: LEFT JOIN

## Topics Covered
- LEFT JOIN
- Preserving all records from the left table
- Finding unmatched records
- Understanding NULL after joins
- Finding customers with and without orders

---

## 1. What is LEFT JOIN?

LEFT JOIN is used to combine two tables based on a related column.

It returns:
- All records from the left table.
- Matching records from the right table.
- NULL values when no matching record exists in the right table.

**Example:**

### Customers Table

| CustomerID | CustomerName |
|---|---|
| 1 | Akash |
| 2 | Priya |
| 3 | Rahul |
| 4 | Sneha |
| 5 | Anjali |

### Orders Table

| OrderID | CustomerID | Amount |
|---|---|---:|
| 101 | 1 | 500 |
| 102 | 2 | 800 |
| 103 | 1 | 300 |
| 104 | 4 | 600 |

## 2. LEFT JOIN Syntax

```sql
SELECT columns
FROM Table1
LEFT JOIN Table2
ON Table1.common_column = Table2.common_column;
```

### Important keywords

| Keyword | Purpose |
|---|---|
| SELECT | Selects columns |
| FROM | Specifies the left table |
| LEFT JOIN | Includes all left-table records |
| ON | Specifies the matching condition |
| NULL | Represents a missing value |

## 3. Practical Example: Display All Customers and Orders

```sql
SELECT
    Customers.CustomerID,
    Customers.CustomerName,
    Orders.OrderID,
    Orders.Amount
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

### Expected Output

| CustomerID | CustomerName | OrderID | Amount |
|---|---|---|---:|
| 1 | Akash | 101 | 500 |
| 1 | Akash | 103 | 300 |
| 2 | Priya | 102 | 800 |
| 3 | Rahul | NULL | NULL |
| 4 | Sneha | 104 | 600 |
| 5 | Anjali | NULL | NULL |

**Observation:** Rahul and Anjali have no orders, but they are still displayed because LEFT JOIN preserves every row from the Customers table.

## 4. Finding Customers Without Orders

We use `IS NULL` to find customers who do not have matching orders.

```sql
SELECT
    Customers.CustomerID,
    Customers.CustomerName
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID = Orders.CustomerID
WHERE Orders.OrderID IS NULL;
```

### Expected Output

| CustomerID | CustomerName |
|---|---|
| 3 | Rahul |
| 5 | Anjali |

**Explanation:** Their OrderID is NULL because they have not placed any orders.

## 5. Finding Customers With Orders

We use `IS NOT NULL` to find customers who have matching orders.

```sql
SELECT
    Customers.CustomerID,
    Customers.CustomerName
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID = Orders.CustomerID
WHERE Orders.OrderID IS NOT NULL;
```

### Expected Output

| CustomerID | CustomerName |
|---|---|
| 1 | Akash |
| 2 | Priya |
| 4 | Sneha |

**Explanation:** These customers have at least one matching order.

## 6. Display All Customers With Their Order Amounts

```sql
SELECT
    Customers.CustomerName,
    Orders.Amount
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

### Expected Output

| CustomerName | Amount |
|---|---:|
| Akash | 500 |
| Akash | 300 |
| Priya | 800 |
| Rahul | NULL |
| Sneha | 600 |
| Anjali | NULL |

## 7. INNER JOIN vs LEFT JOIN

| INNER JOIN | LEFT JOIN |
|---|---|
| Returns matching records only | Returns all left-table records |
| Excludes unmatched left rows | Includes unmatched left rows |
| Does not preserve all left records | Preserves all left records |
| Useful for matching records | Useful for finding missing records |

### Important NULL Conditions

| Condition | Meaning |
|---|---|
| IS NULL | Finds missing values |
| IS NOT NULL | Finds existing values |

**Important:** Never use `= NULL` to check for NULL values. Use `IS NULL` or `IS NOT NULL`.

---

# 8. SQL Practice Questions

Use the Customers and Orders tables given above.

### Q1.
Display all customers along with their order IDs, including customers without orders.

### Q2.
Find customers who have never placed an order.

### Q3.
Find customers who have placed at least one order.

### Q4.
Display all customers and their order amounts. Show NULL for customers without orders.

### Q5.
Find the total number of customers who have not placed any orders.

---

# 9. SQL Practice Solutions

### Solution 1 — Display All Customers and Orders

```sql
SELECT
    Customers.CustomerName,
    Orders.OrderID
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

**Expected unmatched records:** Rahul and Anjali are included with NULL OrderID.

### Solution 2 — Customers Without Orders

```sql
SELECT
    Customers.CustomerName
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID = Orders.CustomerID
WHERE Orders.OrderID IS NULL;
```

**Expected Output:** Rahul, Anjali.

### Solution 3 — Customers With Orders

```sql
SELECT
    Customers.CustomerName
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID = Orders.CustomerID
WHERE Orders.OrderID IS NOT NULL;
```

**Expected Output:** Akash, Priya, Sneha.

### Solution 4 — Display All Customers and Amounts

```sql
SELECT
    Customers.CustomerName,
    Orders.Amount
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

**Expected Output:** All six joined rows, with NULL for Rahul and Anjali.

### Solution 5 — Count Customers Without Orders

```sql
SELECT
    COUNT(*) AS Customers_Without_Orders
FROM Customers
LEFT JOIN Orders
ON Customers.CustomerID = Orders.CustomerID
WHERE Orders.OrderID IS NULL;
```

**Expected Output:**

| Customers_Without_Orders |
|---:|
| 2 |

---

# 10. Key Takeaways

- LEFT JOIN returns all records from the left table.
- Matching records from the right table are included.
- Unmatched right-table values appear as NULL.
- IS NULL helps identify missing or unmatched records.
- IS NOT NULL helps identify matching records.
- LEFT JOIN is useful for customer analysis, missing records and business reporting.

## Day 17 Completion

- [x] Learned LEFT JOIN
- [x] Understood NULL after joins
- [x] Learned to find customers with and without orders
- [x] Practised five SQL questions

**Day 17 — SQL Learning Completed!**
