# Day 3 — SQL Filtering: IN, BETWEEN, LIKE and NULL 🗄️

## 🎯 Learning Objectives

Today, I practised advanced SQL filtering techniques to retrieve specific records from a dataset.

## 📚 Topics Learned

- `IN` — match values from a list
- `BETWEEN` — filter within a range
- `LIKE` — match text patterns
- `%` — match zero or more characters
- `_` — match exactly one character
- `IS NULL` — find missing values
- `IS NOT NULL` — find recorded values

## 📝 Sample Employee Dataset

| Employee_Name | Department | Age | Salary |
|---|---|---:|---:|
| Kiran | Sales | 20 | 35000 |
| Anu | IT | 22 | 30000 |
| Sneha | HR | 24 | 32000 |
| Priya | IT | 25 | 45000 |
| Ravi | HR | 28 | 25000 |

## 💻 SQL Examples

### 1. IN — Match multiple values

```sql
SELECT *
FROM Employee
WHERE Department IN ('IT', 'HR');
```

### 2. BETWEEN — Filter a range

```sql
SELECT *
FROM Employee
WHERE Age BETWEEN 22 AND 25;
```

Both endpoints are included.

### 3. LIKE — Find matching text

```sql
-- Names beginning with A
SELECT * FROM Employee WHERE Employee_Name LIKE 'A%';

-- Names ending with a
SELECT * FROM Employee WHERE Employee_Name LIKE '%a';

-- Names containing i
SELECT * FROM Employee WHERE Employee_Name LIKE '%i%';

-- Names with exactly four characters
SELECT * FROM Employee WHERE Employee_Name LIKE '____';
```

### 4. IS NULL — Find missing values

```sql
SELECT *
FROM Employee
WHERE Salary IS NULL;
```

### 5. IS NOT NULL — Find available values

```sql
SELECT *
FROM Employee
WHERE Salary IS NOT NULL;
```

**Important:** Use `IS NULL` instead of `= NULL`.

## 🧠 Practice Questions

1. Find employees in IT or HR.
2. Find employees in Sales or Finance.
3. Find employees aged between 24 and 28.
4. Find salaries between ₹30,000 and ₹45,000.
5. Find names beginning with A.
6. Find names ending with a.
7. Find names containing i.
8. Find names containing exactly four characters.
9. Find departments beginning with S.
10. Find employees with missing salaries.
11. Find employees whose age is recorded.
12. Find IT employees earning between ₹30,000 and ₹50,000.

## ✅ Practice Answers

```sql
-- 1
SELECT * FROM Employee
WHERE Department IN ('IT', 'HR');

-- 2
SELECT * FROM Employee
WHERE Department IN ('Sales', 'Finance');

-- 3
SELECT * FROM Employee
WHERE Age BETWEEN 24 AND 28;

-- 4
SELECT * FROM Employee
WHERE Salary BETWEEN 30000 AND 45000;

-- 5
SELECT * FROM Employee
WHERE Employee_Name LIKE 'A%';

-- 6
SELECT * FROM Employee
WHERE Employee_Name LIKE '%a';

-- 7
SELECT * FROM Employee
WHERE Employee_Name LIKE '%i%';

-- 8
SELECT * FROM Employee
WHERE Employee_Name LIKE '____';

-- 9
SELECT * FROM Employee
WHERE Department LIKE 'S%';

-- 10
SELECT * FROM Employee
WHERE Salary IS NULL;

-- 11
SELECT * FROM Employee
WHERE Age IS NOT NULL;

-- 12
SELECT * FROM Employee
WHERE Department = 'IT'
AND Salary BETWEEN 30000 AND 50000;
```

**Note:** The sample dataset has no NULL values and no Finance employees. Queries involving those cases are practice examples and may return zero rows.

## 🌍 Connection to Data Analytics

These filtering techniques help analysts find relevant customers, employees, transactions and other records. Pattern matching and NULL checks are particularly useful when exploring and cleaning real-world datasets.

## 🚀 Day 3 Summary

I practised SQL filtering with `IN`, `BETWEEN`, `LIKE`, `IS NULL` and `IS NOT NULL`, and wrote 12 filtering queries.

#SQL #DataAnalytics #DataScience #LearningJourney
