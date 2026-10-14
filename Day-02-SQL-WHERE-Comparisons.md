# Day 2 — WHERE and Comparison Operators 🗄️

## 🎯 Learning Objectives

Today, I learned how to filter employee records using SQL conditions and logical operators.

## 📚 Topics Learned

- `WHERE` clause
- Comparison operators: `=`, `>`, `<`, `>=`, `<=`, `<>`
- Logical operators: `AND`, `OR`, `NOT`
- Filtering employee data by department, age and salary
- Combining multiple conditions

## 🤔 What is WHERE?

The `WHERE` clause filters rows based on a specified condition.

### Example Employee Table

| emp_id | name | department | age | salary |
|---|---|---|---:|---:|
| 101 | Anu | IT | 22 | 30000 |
| 102 | Ravi | HR | 28 | 25000 |
| 103 | Priya | IT | 25 | 45000 |
| 104 | Kiran | Sales | 30 | 35000 |
| 105 | Sneha | HR | 24 | 32000 |
| 106 | Arjun | Sales | 27 | 50000 |

## 🔹 Comparison Operators

| Operator | Meaning |
|---|---|
| `=` | Equal to |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal to |
| `<=` | Less than or equal to |
| `<>` | Not equal to |

## 💻 SQL Examples

### 1. Employees in IT

```sql
SELECT *
FROM Employee
WHERE department = 'IT';
```

### 2. Salary greater than ₹30,000

```sql
SELECT *
FROM Employee
WHERE salary > 30000;
```

### 3. Employees aged 25 or younger

```sql
SELECT *
FROM Employee
WHERE age <= 25;
```

### 4. Employees not in HR

```sql
SELECT *
FROM Employee
WHERE department <> 'HR';
```

## 🔗 Logical Operators

### AND — Both conditions must be true

```sql
SELECT *
FROM Employee
WHERE department = 'IT'
AND salary > 30000;
```

### OR — At least one condition must be true

```sql
SELECT *
FROM Employee
WHERE department = 'HR'
OR salary > 40000;
```

### NOT — Reverses a condition

```sql
SELECT *
FROM Employee
WHERE NOT department = 'IT';
```

## 📝 Practice Questions

1. Find employees earning more than ₹35,000.
2. Find employees aged below 27.
3. Display employees working in HR.
4. Find employees earning ₹30,000 or more.
5. Find employees who are not in Sales.
6. Find IT employees earning more than ₹30,000.
7. Find HR employees or employees earning more than ₹40,000.
8. Find employees aged 25 or above.

## ✅ Practice Answers

```sql
-- 1. Salary greater than 35000
SELECT * FROM Employee WHERE salary > 35000;

-- 2. Age below 27
SELECT * FROM Employee WHERE age < 27;

-- 3. Employees in HR
SELECT * FROM Employee WHERE department = 'HR';

-- 4. Salary 30000 or more
SELECT * FROM Employee WHERE salary >= 30000;

-- 5. Employees not in Sales
SELECT * FROM Employee WHERE department <> 'Sales';

-- 6. IT employees earning more than 30000
SELECT * FROM Employee
WHERE department = 'IT' AND salary > 30000;

-- 7. HR employees or salary greater than 40000
SELECT * FROM Employee
WHERE department = 'HR' OR salary > 40000;

-- 8. Employees aged 25 or above
SELECT * FROM Employee WHERE age >= 25;
```

## 🌍 Connection to Data Analytics

SQL filtering helps analysts retrieve specific records from large datasets. These techniques can be used to analyse salaries, departments, customer purchases and business performance.

## 🚀 Day 2 Summary

I practised SQL filtering with `WHERE`, comparison operators and logical conditions.

**Next:** Continue building my SQL skills with hands-on practice.

#SQL #DataAnalytics #DataScience #LearningJourney
