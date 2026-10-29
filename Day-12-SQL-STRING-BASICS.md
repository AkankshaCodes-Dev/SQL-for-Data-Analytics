# 📘 Day 12 — SQL String Functions

## 🎯 Learning Objectives

In Day 12, I learned how to use SQL string functions to clean, standardize, extract, and combine text data.

These functions are useful when working with customer names, product categories, product codes, and other text fields in real-world datasets.

## 1. What Is a String in SQL?

A **string** is a sequence of characters, such as a name, city, category, or product code.

Examples:
- `'Akanksha'`
- `'Electronics'`
- `'PRD105'`
- `'Ballari'`

String values are generally enclosed in single quotes in SQL.

## 2. UPPER() — Convert Text to Uppercase

**Meaning:** Converts all lowercase letters in a string to uppercase.

**Syntax:**
```sql
UPPER(string);
```

**Example:**
```sql
SELECT UPPER('akanksha') AS customer_name;
```

**Output:**

| customer_name |
|---|
| AKANKSHA |

**Use case:** Standardizing product categories and customer names.

## 3. LOWER() — Convert Text to Lowercase

**Meaning:** Converts all uppercase letters in a string to lowercase.

**Syntax:**
```sql
LOWER(string);
```

**Example:**
```sql
SELECT LOWER('BALLARI') AS city_name;
```

**Output:**

| city_name |
|---|
| ballari |

**Use case:** Making text consistent before comparison or analysis.

## 4. CONCAT() — Combine Strings

**Meaning:** Combines two or more strings into a single string.

**Syntax:**
```sql
CONCAT(string1, string2, ...);
```

**Example:**
```sql
SELECT CONCAT('Akanksha', ' ', 'Sharma')
       AS full_name;
```

**Output:**

| full_name |
|---|
| Akanksha Sharma |

Another example:

```sql
SELECT CONCAT('PRD', '105') AS product_code;
```

Output: `PRD105`

**Use case:** Combining first and last names, or creating customer and product descriptions.

## 5. SUBSTRING() — Extract Part of a String

**Meaning:** Extracts a specified number of characters from a string.

**Syntax:**
```sql
SUBSTRING(string, start_position, length);
```

**Example:**
```sql
SELECT SUBSTRING('PRD105', 4, 3)
       AS product_number;
```

**Output:**

| product_number |
|---|
| 105 |

**Explanation:**
- `'PRD105'` is the original string.
- `4` is the starting position.
- `3` is the number of characters to extract.

SQL dialects may use slightly different syntax or function names. Check your database's documentation when necessary.

## 6. TRIM() — Remove Extra Spaces

**Meaning:** Removes leading and trailing ordinary spaces from a string.

**Syntax:**
```sql
TRIM(string);
```

**Example:**
```sql
SELECT TRIM('   Electronics   ')
       AS category_name;
```

**Output:** `Electronics`

**Use case:** Cleaning imported text containing unwanted spaces.

Note: TRIM does not generally collapse multiple spaces between words into one.

## 7. Combining String Functions

String functions can be combined in a single query.

**Example:**
```sql
SELECT
    UPPER(customer_name) AS customer_name,
    LOWER(city) AS city_name,
    CONCAT(
        UPPER(customer_name),
        ' - ',
        LOWER(city)
    ) AS customer_location
FROM customers;
```

This query:
1. Converts customer names to uppercase.
2. Converts cities to lowercase.
3. Combines the name and city into one field.

## 8. Sample Practice Tables

### Customers

| customer_id | customer_name | city |
|---:|---|---|
| 1 | akanksha sharma | BANGALORE |
| 2 | RAHUL KUMAR | mysore |
| 3 | priya reddy | BALLARI |
| 4 | sneha patil | HUBLI |
| 5 | arjun nair | MANGALORE |

### Products

| product_id | product_code | category |
|---:|---|---|
| 1 | prd101 | electronics |
| 2 | PRD205 | CLOTHING |
| 3 | prd310 | grocery |
| 4 | PRD415 | home decor |
| 5 | prd520 | furniture |

## 9. Practice Questions with Answers

### Q1. Convert customer names to uppercase.

```sql
SELECT UPPER(customer_name) AS customer_name
FROM customers;
```

### Q2. Convert city names to lowercase.

```sql
SELECT LOWER(city) AS city_name
FROM customers;
```

### Q3. Combine customer name and city using a hyphen.

```sql
SELECT CONCAT(customer_name, ' - ', city)
       AS customer_location
FROM customers;
```

### Q4. Convert product categories to uppercase.

```sql
SELECT UPPER(category) AS category_name
FROM products;
```

### Q5. Extract the three-digit number from each product code.

```sql
SELECT SUBSTRING(product_code, 4, 3)
       AS product_number
FROM products;
```

### Q6. Extract the first three characters after converting the product code to uppercase.

```sql
SELECT SUBSTRING(UPPER(product_code), 1, 3)
       AS product_prefix
FROM products;
```

### Q7. Combine product code and category with a colon separator.

```sql
SELECT CONCAT(product_code, ' : ', category)
       AS product_details
FROM products;
```

### Q8. Remove leading and trailing spaces from customer names.

```sql
SELECT TRIM(customer_name) AS customer_name
FROM customers;
```

### Q9. Create a combined field with the uppercase customer name and lowercase city.

```sql
SELECT CONCAT(
    UPPER(customer_name),
    ' - ',
    LOWER(city)
) AS customer_details
FROM customers;
```

### Q10. Extract the first three characters from every product code using SUBSTRING().

```sql
SELECT SUBSTRING(product_code, 1, 3)
       AS product_prefix
FROM products;
```

## 10. Important Notes

- `UPPER()` changes capitalization to uppercase.
- `LOWER()` changes capitalization to lowercase.
- `CONCAT()` joins strings.
- `SUBSTRING()` extracts characters from a string.
- `TRIM()` removes leading and trailing spaces.
- `AS` assigns a meaningful name to a result column.
- SQL function syntax and NULL handling can vary between database systems.

## 🚀 Day 12 Key Takeaway

String functions help transform inconsistent text into cleaner, more standardized data. This is an important step in preparing customer and product datasets for accurate data analysis.

## 📌 Skills Practiced

- SQL string manipulation
- Text standardization
- Data cleaning
- Character extraction
- Combining columns

#SQL #DataAnalytics #LearningSQL #30DaysOfLearning
