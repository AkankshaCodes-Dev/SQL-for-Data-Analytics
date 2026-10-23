# Day 10 — SQL CASE WHEN

## 📌 Overview

On Day 10 of my SQL learning journey, I learned how to use `CASE WHEN` to create categories from data and combine conditional logic with aggregate functions.

### 🎯 Topics Covered

- CASE WHEN, WHEN, THEN, ELSE, and END
- Creating categories using conditions
- Creating salary bands and sales performance categories
- Using CASE WHEN with COUNT(), SUM(), and AVG()
- Grouping categorized results using GROUP BY

## 1. What is CASE WHEN?

`CASE WHEN` is a SQL expression that returns a result based on specified conditions. It works like if-else logic in programming.

### Syntax

```sql
SELECT column_name,
       CASE
           WHEN condition1 THEN result1
           WHEN condition2 THEN result2
           ELSE result3
       END AS category
FROM table_name;
```

### Important keywords

| Keyword | Meaning |
|---|---|
| CASE | Starts the conditional expression |
| WHEN | Specifies a condition |
| THEN | Returns a result when the condition is true |
| ELSE | Returns a default result |
| END | Ends the CASE expression |
| AS | Assigns an alias to the result column |

## 2. Example — Student Performance Categories

```sql
SELECT student_name, marks,
       CASE
           WHEN marks >= 75 THEN 'Excellent'
           WHEN marks >= 60 THEN 'Good'
           WHEN marks >= 35 THEN 'Pass'
           ELSE 'Fail'
       END AS performance
FROM Students;
```

This query categorizes students based on their marks.

**Note:** SQL checks conditions from top to bottom and returns the result of the first matching condition.

## 3. Example — Employee Salary Bands

```sql
SELECT employee_name, salary,
       CASE
           WHEN salary >= 60000 THEN 'High'
           WHEN salary >= 30000 THEN 'Medium'
           ELSE 'Low'
       END AS salary_band
FROM Employees;
```

This query classifies employees into High, Medium, and Low salary bands.

## 4. CASE WHEN with Aggregate Functions

### Count employees in each salary band

```sql
SELECT
    CASE
        WHEN salary >= 60000 THEN 'High'
        WHEN salary >= 30000 THEN 'Medium'
        ELSE 'Low'
    END AS salary_band,
    COUNT(*) AS employee_count
FROM Employees
GROUP BY
    CASE
        WHEN salary >= 60000 THEN 'High'
        WHEN salary >= 30000 THEN 'Medium'
        ELSE 'Low'
    END;
```

### Calculate total salary by salary band

Use `SUM(salary)` instead of `COUNT(*)` to calculate the total salary in each category.

### Calculate average salary by salary band

Use `AVG(salary)` instead of `COUNT(*)` to calculate the average salary in each category.

## 5. Example — Sales Performance Categories

```sql
SELECT
    CASE
        WHEN sales_amount >= 10000 THEN 'High Sales'
        WHEN sales_amount >= 5000 THEN 'Medium Sales'
        ELSE 'Low Sales'
    END AS sales_category,
    SUM(sales_amount) AS total_sales
FROM Sales
GROUP BY
    CASE
        WHEN sales_amount >= 10000 THEN 'High Sales'
        WHEN sales_amount >= 5000 THEN 'Medium Sales'
        ELSE 'Low Sales'
    END;
```

This query categorizes sales transactions and calculates total sales for each category.

## 📝 Practice Tasks and Solutions

### Task 1: Categorize student marks

**Question:** Label marks of 75 or above as Excellent, 60 or above as Good, 35 or above as Pass, and the rest as Fail.

```sql
SELECT student_name, marks,
       CASE
           WHEN marks >= 75 THEN 'Excellent'
           WHEN marks >= 60 THEN 'Good'
           WHEN marks >= 35 THEN 'Pass'
           ELSE 'Fail'
       END AS performance
FROM Students;
```

### Task 2: Create salary bands

```sql
SELECT employee_name, salary,
       CASE
           WHEN salary >= 60000 THEN 'High'
           WHEN salary >= 30000 THEN 'Medium'
           ELSE 'Low'
       END AS salary_band
FROM Employees;
```

### Task 3: Categorize sales transactions

```sql
SELECT sales_amount,
       CASE
           WHEN sales_amount >= 10000 THEN 'High Sales'
           WHEN sales_amount >= 5000 THEN 'Medium Sales'
           ELSE 'Low Sales'
       END AS sales_category
FROM Sales;
```

### Task 4: Display employee names, salaries, and salary bands

```sql
SELECT employee_name, salary,
       CASE
           WHEN salary >= 60000 THEN 'High'
           WHEN salary >= 30000 THEN 'Medium'
           ELSE 'Low'
       END AS salary_band
FROM Employees;
```

### Task 5: Count employees in each salary band

```sql
SELECT
    CASE
        WHEN salary >= 60000 THEN 'High'
        WHEN salary >= 30000 THEN 'Medium'
        ELSE 'Low'
    END AS salary_band,
    COUNT(*) AS employee_count
FROM Employees
GROUP BY
    CASE
        WHEN salary >= 60000 THEN 'High'
        WHEN salary >= 30000 THEN 'Medium'
        ELSE 'Low'
    END;
```

### Task 6: Calculate total salary by salary band

Use the Task 5 query and replace `COUNT(*) AS employee_count` with:

```sql
SUM(salary) AS total_salary
```

### Task 7: Calculate average salary by salary band

Use the Task 5 query and replace `COUNT(*) AS employee_count` with:

```sql
AVG(salary) AS average_salary
```

### Task 8: Create a marks category column

```sql
SELECT student_name, marks,
       CASE
           WHEN marks >= 80 THEN 'Excellent'
           WHEN marks >= 60 THEN 'Good'
           WHEN marks >= 35 THEN 'Pass'
           ELSE 'Fail'
       END AS marks_category
FROM Students;
```

### Task 9: Count sales transactions by category

```sql
SELECT
    CASE
        WHEN sales_amount >= 10000 THEN 'High Sales'
        WHEN sales_amount >= 5000 THEN 'Medium Sales'
        ELSE 'Low Sales'
    END AS sales_category,
    COUNT(*) AS transaction_count
FROM Sales
GROUP BY
    CASE
        WHEN sales_amount >= 10000 THEN 'High Sales'
        WHEN sales_amount >= 5000 THEN 'Medium Sales'
        ELSE 'Low Sales'
    END;
```

### Task 10: Calculate total sales by category

Use the Task 9 query and replace `COUNT(*) AS transaction_count` with:

```sql
SUM(sales_amount) AS total_sales
```

## 💡 Key Learnings

- CASE WHEN creates categories based on conditions.
- ELSE handles values that do not match earlier conditions.
- Conditions are checked from top to bottom.
- COUNT(), SUM(), and AVG() summarize data.
- GROUP BY groups records with the same category.
- CASE WHEN is useful for salary analysis, student performance, and sales reporting.

## 📈 Day 10 Progress

- [x] Learned CASE WHEN syntax
- [x] Practiced creating categories
- [x] Learned salary bands and sales categories
- [x] Practiced CASE WHEN with aggregate functions
- [x] Completed 10 practice tasks and checked solutions

**Next:** Continue learning SQL through practical, beginner-friendly data analysis exercises.
