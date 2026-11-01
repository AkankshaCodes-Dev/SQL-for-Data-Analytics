# Day 14 — SQL Checkpoint 2

## Overview
Today I completed my second SQL checkpoint as part of my Data Analytics learning journey.

This checkpoint tested my understanding of:
- SELECT
- WHERE
- AND
- BETWEEN
- Aggregate functions
- GROUP BY
- HAVING
- CASE WHEN
- ORDER BY
- Date functions

**Result: 20/20 SQL queries completed correctly.**

---

## Sample Dataset: Orders

Table name: `orders`

| order_id | customer | category | amount | city | order_date |
|---|---|---|---:|---|---|
| 101 | Akanksha | Electronics | 25000 | Raichur | 2025-01-10 |
| 102 | Rahul | Clothing | 1500 | Bengaluru | 2025-01-15 |
| 103 | Priya | Electronics | 18000 | Hyderabad | 2025-02-05 |
| 104 | Sneha | Grocery | 800 | Raichur | 2025-02-20 |
| 105 | Arjun | Clothing | 3000 | Bengaluru | 2025-03-10 |
| 106 | Kiran | Grocery | 1200 | Hyderabad | 2025-03-15 |
| 107 | Meena | Electronics | 32000 | Raichur | 2025-04-02 |
| 108 | Rohan | Clothing | 2200 | Hyderabad | 2025-04-12 |
| 109 | Divya | Grocery | 900 | Bengaluru | 2025-05-01 |
| 110 | Varun | Electronics | 15000 | Raichur | 2025-05-18 |

---

## 1. SELECT and Filtering

### Meaning
- `SELECT` retrieves data from a table.
- `WHERE` filters records based on a condition.
- `AND` checks whether multiple conditions are true.
- `BETWEEN` selects values within a specified range, including both endpoints.

### Syntax

```sql
SELECT column_name
FROM table_name
WHERE condition;
```

### Practice Questions and Answers

**Q1. Display all columns from the orders table.**

```sql
SELECT *
FROM orders;
```

**Q2. Display only customer names and amounts.**

```sql
SELECT customer, amount
FROM orders;
```

**Q3. Find orders where amount is greater than 5,000.**

```sql
SELECT *
FROM orders
WHERE amount > 5000;
```

**Q4. Find orders from Raichur.**

```sql
SELECT *
FROM orders
WHERE city = 'Raichur';
```

**Q5. Find orders where amount is between 1,000 and 20,000.**

```sql
SELECT *
FROM orders
WHERE amount >= 1000 AND amount <= 20000;
```

Alternative:

```sql
SELECT *
FROM orders
WHERE amount BETWEEN 1000 AND 20000;
```

---

## 2. Aggregate Functions

### Meaning
Aggregate functions perform calculations on multiple rows and return a single result.

| Function | Meaning |
|---|---|
| COUNT() | Counts records |
| SUM() | Calculates total |
| AVG() | Calculates average |
| MAX() | Finds highest value |
| MIN() | Finds lowest value |

### Syntax

```sql
SELECT COUNT(*)
FROM table_name;
```

### Practice Questions and Answers

**Q6. Find the total number of orders.**

```sql
SELECT COUNT(*) AS total_orders
FROM orders;
```

Output: 10

**Q7. Calculate total sales.**

```sql
SELECT SUM(amount) AS total_sales
FROM orders;
```

Output: ₹100,600

**Q8. Find average order amount.**

```sql
SELECT AVG(amount) AS average_amount
FROM orders;
```

Output: ₹10,060

**Q9. Find the highest order amount.**

```sql
SELECT MAX(amount) AS highest_amount
FROM orders;
```

Output: ₹32,000

**Q10. Find the lowest order amount.**

```sql
SELECT MIN(amount) AS lowest_amount
FROM orders;
```

Output: ₹800

---

## 3. GROUP BY

### Meaning
`GROUP BY` groups rows that have the same value so aggregate functions can calculate results for each group.

### Syntax

```sql
SELECT column_name, AGGREGATE_FUNCTION(column_name)
FROM table_name
GROUP BY column_name;
```

### Practice Questions and Answers

**Q11. Find total sales for each city.**

```sql
SELECT city, SUM(amount) AS total_sales
FROM orders
GROUP BY city;
```

Expected output:

| City | Total sales |
|---|---:|
| Raichur | 72000 |
| Bengaluru | 5400 |
| Hyderabad | 22700 |

**Q12. Count the number of orders in each category.**

```sql
SELECT category, COUNT(*) AS order_count
FROM orders
GROUP BY category;
```

Expected output:

| Category | Order count |
|---|---:|
| Electronics | 4 |
| Clothing | 3 |
| Grocery | 3 |

**Q13. Find average order amount for each category.**

```sql
SELECT category, AVG(amount) AS average_amount
FROM orders
GROUP BY category;
```

Expected output:

| Category | Average amount |
|---|---:|
| Electronics | 22500 |
| Clothing | 2233.33 |
| Grocery | 966.67 |

**Q14. Display total sales for each month using MONTH().**

```sql
SELECT MONTH(order_date) AS order_month,
       SUM(amount) AS total_sales
FROM orders
GROUP BY MONTH(order_date);
```

Expected output:

| Month | Total sales |
|---|---:|
| 1 | 26500 |
| 2 | 18800 |
| 3 | 4200 |
| 4 | 34200 |
| 5 | 15900 |

---

## 4. HAVING

### Meaning
`HAVING` filters grouped results after `GROUP BY`.

### Difference between WHERE and HAVING

| WHERE | HAVING |
|---|---|
| Filters individual rows | Filters groups |
| Applied before grouping | Applied after grouping |
| Commonly used with row conditions | Commonly used with aggregate conditions |

### Syntax

```sql
SELECT column_name, SUM(amount)
FROM table_name
GROUP BY column_name
HAVING SUM(amount) > value;
```

### Practice Questions and Answers

**Q15. Display cities whose total sales are greater than ₹20,000.**

```sql
SELECT city, SUM(amount) AS total_sales
FROM orders
GROUP BY city
HAVING SUM(amount) > 20000;
```

Expected cities: Raichur and Hyderabad.

**Q16. Display categories having more than 2 orders.**

```sql
SELECT category, COUNT(*) AS order_count
FROM orders
GROUP BY category
HAVING COUNT(*) > 2;
```

Expected categories: Electronics, Clothing and Grocery.

---

## 5. CASE WHEN

### Meaning
`CASE WHEN` is used to apply conditions and return different results based on those conditions.

### Syntax

```sql
CASE
    WHEN condition THEN result
    WHEN condition THEN result
    ELSE default_result
END
```

### Practice Questions and Answers

**Q17. Classify orders as High, Medium or Low.**

Conditions:
- Amount above ₹20,000 = High
- Amount above ₹5,000 = Medium
- Otherwise = Low

```sql
SELECT *,
    CASE
        WHEN amount > 20000 THEN 'High'
        WHEN amount > 5000 THEN 'Medium'
        ELSE 'Low'
    END AS order_classification
FROM orders;
```

**Q18. Count how many orders belong to each sales category.**

```sql
SELECT
    CASE
        WHEN amount > 20000 THEN 'High'
        WHEN amount > 5000 THEN 'Medium'
        ELSE 'Low'
    END AS sales_category,
    COUNT(*) AS order_count
FROM orders
GROUP BY
    CASE
        WHEN amount > 20000 THEN 'High'
        WHEN amount > 5000 THEN 'Medium'
        ELSE 'Low'
    END;
```

Expected output:

| Sales category | Order count |
|---|---:|
| High | 2 |
| Medium | 3 |
| Low | 5 |

---

## 6. Mixed SQL Queries

**Q19. Find total sales for Electronics orders in Raichur.**

```sql
SELECT SUM(amount) AS total_electronics_sales
FROM orders
WHERE category = 'Electronics'
AND city = 'Raichur';
```

Output: ₹72,000

**Q20. Display categories whose average order amount is greater than ₹5,000, in descending order.**

```sql
SELECT category, AVG(amount) AS average_amount
FROM orders
GROUP BY category
HAVING AVG(amount) > 5000
ORDER BY average_amount DESC;
```

Expected output:

| Category | Average amount |
|---|---:|
| Electronics | 22500 |

---

## Key Learnings

- Retrieved data using SELECT.
- Filtered records using WHERE, AND and BETWEEN.
- Performed calculations using aggregate functions.
- Grouped data using GROUP BY.
- Filtered grouped results using HAVING.
- Classified orders using CASE WHEN.
- Sorted results using ORDER BY.
- Combined SQL concepts to solve business questions.

## Checkpoint Result

**20/20 — All 20 SQL queries completed correctly.**

This checkpoint helped me improve my SQL problem-solving skills and prepare for practical Data Analyst tasks.

#SQL #DataAnalytics #DataAnalyst #LearningJourney
