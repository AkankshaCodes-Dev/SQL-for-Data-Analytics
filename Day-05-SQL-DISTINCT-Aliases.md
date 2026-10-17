
# Day 5 — SQL DISTINCT and Column Aliases

## 1. Learning Objectives

- Understand the `DISTINCT` keyword.
- Retrieve unique departments, cities, and job roles.
- Understand column aliases using `AS`.
- Rename columns to make query output readable.
- Practice SQL queries using an employee dataset.

## 2. Sample Dataset

Table name: `employees`

| employee_name | department | city | job_role |
|---|---|---|---|
| Anu | IT | Ballari | Analyst |
| Ravi | Sales | Bengaluru | Manager |
| Priya | IT | Ballari | Developer |
| Kiran | HR | Mysuru | Recruiter |
| Meena | Sales | Bengaluru | Analyst |

## 3. DISTINCT Keyword

### Definition

`DISTINCT` is an SQL keyword used to return only unique values from a column or combination of columns. Duplicate rows in the selected results are eliminated.

### Syntax

    SELECT DISTINCT column_name
    FROM table_name;

### Example 1: Find Unique Departments

    SELECT DISTINCT department
    FROM employees;

### Output

| department |
|---|
| IT |
| Sales |
| HR |

Explanation: IT and Sales occur more than once in the original table, but each appears only once in the result.

### Example 2: Find Unique Cities

    SELECT DISTINCT city
    FROM employees;

### Output

| city |
|---|
| Ballari |
| Bengaluru |
| Mysuru |

### Example 3: Find Unique Job Roles

    SELECT DISTINCT job_role
    FROM employees;

### Output

| job_role |
|---|
| Analyst |
| Manager |
| Developer |
| Recruiter |

### Example 4: Find Unique Department and City Combinations

    SELECT DISTINCT department, city
    FROM employees;

Explanation: DISTINCT considers the combination of both selected columns. Different department-city combinations are returned separately.

### Uses of DISTINCT

- Identifying unique categories.
- Finding the different cities in a dataset.
- Exploring departments or job roles.
- Removing duplicate combinations from query results.

## 4. Column Aliases Using AS

### Definition

A column alias is a temporary alternative name assigned to a column or calculated expression in a query result. The `AS` keyword makes the alias explicit.

An alias changes the displayed column heading, not the original column name in the database.

### Syntax

    SELECT column_name AS alias_name
    FROM table_name;

### Example 1: Rename Employee and Department Columns

    SELECT employee_name AS Employee,
           department AS Department
    FROM employees;

### Output

| Employee | Department |
|---|---|
| Anu | IT |
| Ravi | Sales |
| Priya | IT |
| Kiran | HR |
| Meena | Sales |

Explanation: The output headings are Employee and Department instead of employee_name and department.

### Example 2: Rename a Job Role Column

    SELECT employee_name AS Name,
           job_role AS Role
    FROM employees;

### Example 3: Alias a Calculated Result

    SELECT COUNT(*) AS Total_Employees
    FROM employees;

### Output

| Total_Employees |
|---:|
| 5 |

Explanation: COUNT(*) counts all rows in the table, and AS assigns a readable name to the result.

### Why Use Aliases?

- Make output easier to understand.
- Replace long column names with short names.
- Improve report readability.
- Give meaningful names to calculated values.

## 5. Practice Questions

Use the `employees` table to solve these questions.

1. Display all unique departments.
2. Display all unique cities.
3. Display all unique job roles.
4. Display employee names using the alias `Employee_Name`.
5. Display department values using the alias `Department_Name`.
6. Display employee names as `Name` and job roles as `Role`.
7. Count all employees and name the result `Total_Employees`.

## 6. Practice Solutions

### Solution 1: Unique Departments

    SELECT DISTINCT department
    FROM employees;

### Solution 2: Unique Cities

    SELECT DISTINCT city
    FROM employees;

### Solution 3: Unique Job Roles

    SELECT DISTINCT job_role
    FROM employees;

### Solution 4: Alias Employee Names

    SELECT employee_name AS Employee_Name
    FROM employees;

### Solution 5: Alias Department Names

    SELECT department AS Department_Name
    FROM employees;

### Solution 6: Rename Two Output Columns

    SELECT employee_name AS Name,
           job_role AS Role
    FROM employees;

### Solution 7: Count Employees

    SELECT COUNT(*) AS Total_Employees
    FROM employees;

## 7. Key Takeaways

- `DISTINCT` returns unique selected values or combinations.
- `AS` provides a readable alias for a column or expression.
- Aliases do not permanently rename database columns.
- `COUNT(*)` counts rows in a table.
- Clear output headings make SQL reports easier to interpret.

## 8. Data Analytics Connection

A Data Analyst may use DISTINCT to identify the different categories in a dataset before performing analysis. Column aliases help present query results clearly in reports and dashboards.

## 9. Day 5 Completion

- [ ] Learned DISTINCT.
- [ ] Practiced unique departments, cities, and job roles.
- [ ] Learned aliases using AS.
- [ ] Completed practice queries.
