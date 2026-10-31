# 📘 Day 13 — SQL Date Functions

## 🎯 Learning Objectives

In Day 13, I learned how to work with dates in SQL using date functions and filtering conditions.

I practiced extracting years, months and days, filtering records by date ranges, and analyzing orders based on monthly and yearly performance.

Date functions are important in Data Analytics because businesses need to understand sales trends, customer transactions and performance over time.

## 1. What Is a Date in SQL?

A date represents a specific day, month and year.

**Examples:**
- `2025-01-10`
- `2025-02-15`
- `2026-10-31`

The commonly used SQL date format is:

`YYYY-MM-DD`

| Component | Example |
|---|---|
| Year | 2025 |
| Month | 01 |
| Day | 10 |

## 2. WHERE — Filter Records by Date

**Meaning:** WHERE filters records based on a specified condition.

**Syntax:**
```sql
SELECT column_name
FROM table_name
WHERE date_column = 'YYYY-MM-DD';
```

**Example:**

Find orders placed on 10 January 2025.

```sql
SELECT *
FROM orders
WHERE order_date = '2025-01-10';
```

**Expected Output:**

| order_id | customer_name | order_date | amount |
|---:|---|---|---:|
| 101 | Akanksha | 2025-01-10 | 1200 |

**Use case:** Finding transactions made on a particular date.

## 3. BETWEEN — Filter a Date Range

**Meaning:** BETWEEN selects records within a specified range, including both endpoints.

**Syntax:**
```sql
SELECT *
FROM table_name
WHERE date_column BETWEEN 'start_date' AND 'end_date';
```

**Example:**

Find orders placed during January 2025.

```sql
SELECT *
FROM orders
WHERE order_date
BETWEEN '2025-01-01' AND '2025-01-31';
```

**Expected Output:**

| order_id | customer_name | order_date |
|---:|---|---|
| 101 | Akanksha | 2025-01-10 |
| 102 | Rahul | 2025-01-20 |

**Use case:** Finding transactions within a particular month or period.

**Important:** When a column stores timestamps, use an inclusive start and exclusive end condition to include the entire final day.

```sql
WHERE order_date >= '2025-01-01'
AND order_date < '2025-02-01';
```

## 4. YEAR() — Extract the Year

**Meaning:** YEAR() extracts the year portion from a date.

**Syntax (MySQL):**
```sql
YEAR(date_column);
```

**Example:**
```sql
SELECT
    order_date,
    YEAR(order_date) AS order_year
FROM orders;
```

**Expected Output:**

| order_date | order_year |
|---|---:|
| 2025-01-10 | 2025 |
| 2025-02-05 | 2025 |
| 2026-01-12 | 2026 |

**Use case:** Comparing business performance across different years.

## 5. MONTH() — Extract the Month

**Meaning:** MONTH() extracts the month number from a date.

**Syntax (MySQL):**
```sql
MONTH(date_column);
```

**Example:**
```sql
SELECT
    order_date,
    MONTH(order_date) AS order_month
FROM orders;
```

**Expected Output:**

| order_date | order_month |
|---|---:|
| 2025-01-10 | 1 |
| 2025-02-05 | 2 |
| 2025-03-15 | 3 |

**Month number reference:**

| Month | Number |
|---|---:|
| January | 1 |
| February | 2 |
| March | 3 |
| April | 4 |
| May | 5 |
| June | 6 |
| July | 7 |
| August | 8 |
| September | 9 |
| October | 10 |
| November | 11 |
| December | 12 |

**Use case:** Analyzing monthly sales trends.

## 6. DAY() — Extract the Day

**Meaning:** DAY() extracts the day of the month from a date.

**Syntax (MySQL):**
```sql
DAY(date_column);
```

**Example:**
```sql
SELECT
    order_date,
    DAY(order_date) AS order_day
FROM orders;
```

**Expected Output:**

| order_date | order_day |
|---|---:|
| 2025-01-10 | 10 |
| 2025-02-05 | 5 |
| 2025-03-15 | 15 |

**Use case:** Analyzing transactions based on the day of the month.

## 7. GROUP BY with YEAR() and MONTH()

**Meaning:** GROUP BY combines records with the same year and month into groups.

**Example:**

Count the number of orders placed in each month and year.

```sql
SELECT
    YEAR(order_date) AS order_year,
    MONTH(order_date) AS order_month,
    COUNT(*) AS total_orders
FROM orders
GROUP BY
    YEAR(order_date),
    MONTH(order_date)
ORDER BY
    order_year,
    order_month;
```

**Expected Output:**

| order_year | order_month | total_orders |
|---:|---:|---:|
| 2025 | 1 | 2 |
| 2025 | 2 | 1 |
| 2025 | 3 | 2 |
| 2026 | 1 | 1 |
| 2026 | 2 | 2 |

**Explanation:**
- YEAR() extracts the year.
- MONTH() extracts the month.
- COUNT() counts the orders.
- GROUP BY groups records by year and month.
- ORDER BY sorts the results chronologically.

## 8. SUM() with Date Grouping

**Meaning:** SUM() adds numeric values, such as order amounts, within each group.

**Example:**

Calculate total revenue for each month and year.

```sql
SELECT
    YEAR(order_date) AS order_year,
    MONTH(order_date) AS order_month,
    SUM(amount) AS total_revenue
FROM orders
GROUP BY
    YEAR(order_date),
    MONTH(order_date)
ORDER BY
    order_year,
    order_month;
```

**Expected Output:**

| order_year | order_month | total_revenue |
|---:|---:|---:|
| 2025 | 1 | 3700 |
| 2025 | 2 | 1800 |
| 2025 | 3 | 4500 |
| 2026 | 1 | 2200 |
| 2026 | 2 | 5200 |

**Use case:** Preparing monthly and yearly sales reports.

## 9. Sample Practice Dataset

Table name: `orders`

| order_id | customer_name | order_date | amount |
|---:|---|---|---:|
| 101 | Akanksha | 2025-01-10 | 1200 |
| 102 | Rahul | 2025-01-20 | 2500 |
| 103 | Priya | 2025-02-05 | 1800 |
| 104 | Sneha | 2025-03-15 | 3000 |
| 105 | Arjun | 2025-03-25 | 1500 |
| 106 | Kiran | 2026-01-12 | 2200 |
| 107 | Meena | 2026-02-18 | 3500 |
| 108 | Rohan | 2026-02-25 | 1700 |

## 10. SQL Practice Questions with Answers

### Q1. Display all orders placed on 10 January 2025.

```sql
SELECT *
FROM orders
WHERE order_date = '2025-01-10';
```

**Output:** Order ID 101 — Akanksha.

### Q2. Display orders placed during January 2025.

```sql
SELECT *
FROM orders
WHERE order_date BETWEEN '2025-01-01' AND '2025-01-31';
```

**Output:** Orders 101 and 102.

### Q3. Display all orders placed in the year 2025.

```sql
SELECT *
FROM orders
WHERE order_date BETWEEN '2025-01-01' AND '2025-12-31';
```

**Output:** Orders 101, 102, 103, 104 and 105.

Alternative using YEAR():

```sql
SELECT *
FROM orders
WHERE YEAR(order_date) = 2025;
```

### Q4. Extract the year from every order_date.

```sql
SELECT
    order_date,
    YEAR(order_date) AS order_year
FROM orders;
```

### Q5. Extract the month from every order_date.

```sql
SELECT
    order_date,
    MONTH(order_date) AS order_month
FROM orders;
```

### Q6. Extract the day from every order_date.

```sql
SELECT
    order_date,
    DAY(order_date) AS order_day
FROM orders;
```

### Q7. Count the total orders placed in each year.

```sql
SELECT
    YEAR(order_date) AS order_year,
    COUNT(*) AS total_orders
FROM orders
GROUP BY YEAR(order_date);
```

**Expected Output:**

| order_year | total_orders |
|---:|---:|
| 2025 | 5 |
| 2026 | 3 |

### Q8. Calculate total revenue for each month and year.

```sql
SELECT
    YEAR(order_date) AS order_year,
    MONTH(order_date) AS order_month,
    SUM(amount) AS total_revenue
FROM orders
GROUP BY
    YEAR(order_date),
    MONTH(order_date)
ORDER BY
    order_year,
    order_month;
```

**Expected Output:**

| order_year | order_month | total_revenue |
|---:|---:|---:|
| 2025 | 1 | 3700 |
| 2025 | 2 | 1800 |
| 2025 | 3 | 4500 |
| 2026 | 1 | 2200 |
| 2026 | 2 | 5200 |

### Q9. Find all orders placed between 1 February and 31 March 2025.

```sql
SELECT *
FROM orders
WHERE order_date BETWEEN '2025-02-01' AND '2025-03-31';
```

**Output:** Orders 103, 104 and 105.

### Q10. Count how many orders were placed in each month of each year.

```sql
SELECT
    YEAR(order_date) AS order_year,
    MONTH(order_date) AS order_month,
    COUNT(*) AS total_orders
FROM orders
GROUP BY
    YEAR(order_date),
    MONTH(order_date)
ORDER BY
    order_year,
    order_month;
```

**Expected Output:**

| order_year | order_month | total_orders |
|---:|---:|---:|
| 2025 | 1 | 2 |
| 2025 | 2 | 1 |
| 2025 | 3 | 2 |
| 2026 | 1 | 1 |
| 2026 | 2 | 2 |

## 11. Important SQL Date Concepts — Quick Revision

| Function / Keyword | Purpose |
|---|---|
| WHERE | Filters records |
| BETWEEN | Filters a range |
| YEAR() | Extracts year |
| MONTH() | Extracts month |
| DAY() | Extracts day |
| GROUP BY | Groups records |
| ORDER BY | Sorts records |
| COUNT() | Counts records |
| SUM() | Calculates total |

## 12. Day 13 Key Takeaway

Date functions help transform transaction dates into meaningful business information.

By using date filtering, YEAR(), MONTH(), DAY(), GROUP BY and aggregate functions, I can analyze monthly and yearly sales performance.

## 📌 Skills Practiced

- SQL date filtering
- Date range analysis
- Extracting year, month and day
- Monthly order analysis
- Yearly order analysis
- Revenue aggregation
- Business reporting

#SQL #DataAnalytics #SQLLearning #30DaysOfLearning
