### ORDER BY Challenges ###

-- Challenge 1 \
-- Write a query that returns employees ordered alphabetically by their last name from A to Z:

**Solution:**
```sql
SELECT *
FROM hcm.employees
ORDER BY last_name ASC;
```

-- Challenge 2 \
-- Write a query that returns employees ordered by salary from highest to lowest:

**Solution:**
```sql
SELECT *
FROM hcm.employees
ORDER BY salary DESC;
```

-- Challenge 3 \
-- Write a query that returns employees ordered by most recently hired to longest serving:

**Solution:**
```sql
SELECT *
FROM hcm.employees
ORDER BY hire_date DESC;
```

-- Challenge 4 \
-- Return employees ordered by department_id in ascending order and within each department_id order by salary from highest to lowest:

**Solution:**
```sql
SELECT *
FROM hcm.employees
ORDER BY department_id ASC, salary DESC;
```

-- Challenge 5 \
-- Return the employee ids, names and salaries for the top 10 employees who get paid the most:

**Solution:**
```sql
SELECT TOP (10) employee_id, first_name, last_name, salary
FROM hcm.employees
ORDER BY salary DESC;
```

-- Challenge 6 \
-- Return the employee ids, names and salaries for the employee or employees who get paid the least

**Solution:**
```sql
SELECT TOP (1) WITH TIES employee_id, first_name, last_name, salary
FROM hcm.employees
ORDER BY salary ASC;
```

### WHERE Challenges ###

-- Challenge 1 \
-- Select all products which have a price greater than $100:

**Solution:**
```sql
SELECT *
FROM oes.products
WHERE list_price > 100;
```

-- Challenge 2 \
-- Select all unshipped orders (i.e. where shipped_date is null):

**Solution:**
```sql
SELECT *
FROM oes.orders
WHERE shipped_date IS NULL;
```

-- Challenge 3 \
-- Select all orders placed on the 26th of February 2020: 

**Solution:**
```sql
SELECT *
FROM oes.orders
WHERE order_date = '20200226';
```

-- Challenge 4 \
-- Select all orders placed on or after the 1st of January 2020:

**Solution:**
```sql
SELECT *
FROM oes.orders
WHERE order_date >= '20200101';
```

### Pattern Matching Challenges ###

-- Challenge 1 \
-- Select all countries which start with the letter 'N':

**Solution:**
```sql
SELECT *
FROM hcm.countries
WHERE country_name LIKE 'N%';
```

-- Challenge 2 \
-- Select all customers who have gmail email addresses:

**Solution:**
```sql
SELECT 
	customer_id,
	first_name,
	last_name,
	email
FROM oes.customers
WHERE email LIKE '%@gmail.com';
```

-- Challenge 3 \
-- Select all product names which contain the word 'mouse':

**Solution:**
```sql
SELECT product_name
FROM oes.products
WHERE product_name LIKE '%mouse%';
```

-- Challenge 4 \
-- Select all product names which end in a number:

**Solution:**
```sql
SELECT product_name
FROM oes.products
WHERE product_name LIKE '%[0-9]';
```
