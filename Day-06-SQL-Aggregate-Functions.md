
# Day 6 — SQL Aggregate Functions

## 1. Learning Objectives

- Understand SQL aggregate functions.
- Use COUNT(), SUM(), AVG(), MIN(), and MAX().
- Filter records using WHERE.
- Calculate department-wise statistics using GROUP BY.
- Analyze employee salary data with SQL queries.

## 2. Sample Dataset

Table name: employees

| employee_name | department | city | salary |
|---|---|---|---:|
| Anu | IT | Ballari | 30000 |
| Ravi | Sales | Bengaluru | 35000 |
| Priya | IT | Ballari | 40000 |
| Kiran | HR | Mysuru | 25000 |
| Meena | Sales | Bengaluru | 30000 |
| Arjun | IT | Mysuru | 45000 |

## 3. What Are Aggregate Functions?

Definition:
Aggregate functions perform calculations on multiple rows and return a single result for the selected data or group.

The five important aggregate functions are:

- COUNT() — counts rows or non-NULL values.
- SUM() — calculates a numerical total.
- AVG() — calculates the arithmetic mean.
- MIN() — returns the smallest value.
- MAX() — returns the largest value.

## 4. COUNT() Function

### Definition

COUNT() counts rows or non-NULL values, depending on the expression used.

### Syntax

    SELECT COUNT(expression)
    FROM table_name;

### Example 1: Count All Employees

    SELECT COUNT(*) AS Total_Employees
    FROM employees;

### Expected Output

| Total_Employees |
|---:|
| 6 |

Explanation: COUNT(*) counts all rows, including rows that contain NULL values in individual columns.

### Example 2: Count Employees With a Salary

    SELECT COUNT(salary) AS Employees_With_Salary
    FROM employees;

Expected output: 6

Explanation: COUNT(salary) counts only rows where salary is not NULL.

## 5. SUM() Function

### Definition

SUM() adds the non-NULL numerical values in a selected column.

### Syntax

    SELECT SUM(column_name)
    FROM table_name;

### Example: Calculate Total Salary

    SELECT SUM(salary) AS Total_Salary
    FROM employees;

### Expected Output

| Total_Salary |
|---:|
| 205000 |

Explanation: The combined salary of all six employees is 205,000.

## 6. AVG() Function

### Definition

AVG() calculates the arithmetic mean of non-NULL numerical values.

### Syntax

    SELECT AVG(column_name)
    FROM table_name;

### Example: Calculate Average Salary

    SELECT AVG(salary) AS Average_Salary
    FROM employees;

### Expected Output

| Average_Salary |
|---:|
| 34166.67 |

Explanation: The total salary is divided by the six salary values.

## 7. MIN() Function

### Definition

MIN() returns the smallest value in the selected column.

### Syntax

    SELECT MIN(column_name)
    FROM table_name;

### Example: Find the Lowest Salary

    SELECT MIN(salary) AS Minimum_Salary
    FROM employees;

Expected output: 25000

## 8. MAX() Function

### Definition

MAX() returns the largest value in the selected column.

### Syntax

    SELECT MAX(column_name)
    FROM table_name;

### Example: Find the Highest Salary

    SELECT MAX(salary) AS Maximum_Salary
    FROM employees;

Expected output: 45000

## 9. Using Aggregate Functions With WHERE

### Definition of WHERE

WHERE filters rows according to a specified condition before the aggregate calculation is performed.

### Example 1: Count IT Employees

    SELECT COUNT(*) AS IT_Employee_Count
    FROM employees
    WHERE department = 'IT';

Expected output: 3

### Example 2: Calculate Total Sales Department Salary

    SELECT SUM(salary) AS Sales_Total_Salary
    FROM employees
    WHERE department = 'Sales';

Expected output: 65000

### Example 3: Calculate Average HR Salary

    SELECT AVG(salary) AS HR_Average_Salary
    FROM employees
    WHERE department = 'HR';

Expected output: 25000

### Example 4: Find the Highest IT Salary

    SELECT MAX(salary) AS Highest_IT_Salary
    FROM employees
    WHERE department = 'IT';

Expected output: 45000

## 10. GROUP BY Clause

### Definition

GROUP BY groups rows with matching values in one or more columns. Aggregate functions can then calculate separate results for each group.

### Syntax

    SELECT group_column, aggregate_function(column_name)
    FROM table_name
    GROUP BY group_column;

### Example 1: Count Employees in Each Department

    SELECT department,
           COUNT(*) AS Employee_Count
    FROM employees
    GROUP BY department;

### Expected Output

| department | Employee_Count |
|---|---:|
| HR | 1 |
| IT | 3 |
| Sales | 2 |

The output order is not guaranteed without ORDER BY.

### Example 2: Department-Wise Salary Statistics

    SELECT department,
           COUNT(*) AS Employee_Count,
           SUM(salary) AS Total_Salary,
           AVG(salary) AS Average_Salary,
           MIN(salary) AS Minimum_Salary,
           MAX(salary) AS Maximum_Salary
    FROM employees
    GROUP BY department;

### Expected Output

| department | Employee_Count | Total_Salary | Average_Salary | Minimum_Salary | Maximum_Salary |
|---|---:|---:|---:|---:|---:|
| HR | 1 | 25000 | 25000 | 25000 | 25000 |
| IT | 3 | 115000 | 38333.33 | 30000 | 45000 |
| Sales | 2 | 65000 | 32500 | 30000 | 35000 |

## 11. WHERE vs GROUP BY

| WHERE | GROUP BY |
|---|---|
| Filters individual rows. | Creates groups of matching values. |
| Applied before aggregation. | Calculates separate aggregate results per group. |
| Example: select IT employees. | Example: calculate totals for every department. |

### Example: Filter Before Aggregation

    SELECT SUM(salary) AS IT_Total_Salary
    FROM employees
    WHERE department = 'IT';

Expected output: 115000

### Example: Aggregate by Department

    SELECT department, SUM(salary) AS Total_Salary
    FROM employees
    GROUP BY department;

This returns a separate total for HR, IT, and Sales.

## 12. Practice Questions

Using the employees table:

1. Count all employees.
2. Calculate the total salary of all employees.
3. Find the average salary of all employees.
4. Find the minimum salary.
5. Find the maximum salary.
6. Calculate total salary for Sales employees only.
7. Calculate average salary for HR employees only.
8. Find the highest salary among IT employees.
9. Display each department and its employee count.
10. Display department-wise employee counts, total salary, average salary, minimum salary, and maximum salary.

## 13. Practice Solutions

### Solution 1: Count Employees

    SELECT COUNT(*) AS Total_Employees
    FROM employees;

Result: 6

### Solution 2: Total Salary

    SELECT SUM(salary) AS Total_Salary
    FROM employees;

Result: 205000

### Solution 3: Average Salary

    SELECT AVG(salary) AS Average_Salary
    FROM employees;

Result: 34166.67 approximately

### Solution 4: Minimum Salary

    SELECT MIN(salary) AS Minimum_Salary
    FROM employees;

Result: 25000

### Solution 5: Maximum Salary

    SELECT MAX(salary) AS Maximum_Salary
    FROM employees;

Result: 45000

### Solution 6: Total Sales Salary

    SELECT SUM(salary) AS Sales_Total_Salary
    FROM employees
    WHERE department = 'Sales';

Result: 65000

### Solution 7: Average HR Salary

    SELECT AVG(salary) AS HR_Average_Salary
    FROM employees
    WHERE department = 'HR';

Result: 25000

### Solution 8: Highest IT Salary

    SELECT MAX(salary) AS Highest_IT_Salary
    FROM employees
    WHERE department = 'IT';

Result: 45000

### Solution 9: Department Employee Counts

    SELECT department,
           COUNT(*) AS Employee_Count
    FROM employees
    GROUP BY department;

### Solution 10: Department Salary Statistics

    SELECT department,
           COUNT(*) AS Employee_Count,
           SUM(salary) AS Total_Salary,
           AVG(salary) AS Average_Salary,
           MIN(salary) AS Minimum_Salary,
           MAX(salary) AS Maximum_Salary
    FROM employees
    GROUP BY department;

## 14. Key Takeaways

- COUNT() counts rows or non-NULL values.
- SUM() calculates totals.
- AVG() calculates averages.
- MIN() and MAX() find the smallest and largest values.
- WHERE filters rows before aggregation.
- GROUP BY calculates separate statistics for each group.
- Aliases make result columns easier to understand.

## 15. Data Analytics Applications

SQL aggregate functions help Data Analysts summarize large datasets, compare department performance, calculate salary statistics, and prepare reports for business decisions.

## 16. Day 6 Completion

- [ ] Learned the five aggregate functions.
- [ ] Practiced WHERE with aggregate functions.
- [ ] Learned GROUP BY.
- [ ] Completed department-wise salary analysis.
- [ ] Practiced all ten questions.
