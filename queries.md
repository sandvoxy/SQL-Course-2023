
## ORDER BY Challenges ##

### Challenge 1 ###
* Write a query that returns employees ordered alphabetically by their last name from A to Z:

**Solution:**
```sql
SELECT *
FROM hcm.employees
ORDER BY last_name ASC;
```

### Challenge 2 ###
* Write a query that returns employees ordered by salary from highest to lowest:

**Solution:**
```sql
SELECT *
FROM hcm.employees
ORDER BY salary DESC;
```

### Challenge 3 ###
* Write a query that returns employees ordered by most recently hired to longest serving:

**Solution:**
```sql
SELECT *
FROM hcm.employees
ORDER BY hire_date DESC;
```

### Challenge 4 ###
* Return employees ordered by department_id in ascending order and within each department_id order by salary from highest to lowest:

**Solution:**
```sql
SELECT *
FROM hcm.employees
ORDER BY department_id ASC, salary DESC;
```

### Challenge 5 ###
* Return the employee ids, names and salaries for the top 10 employees who get paid the most:

**Solution:**
```sql
SELECT TOP (10) employee_id, first_name, last_name, salary
FROM hcm.employees
ORDER BY salary DESC;
```

### Challenge 6 ###
* Return the employee ids, names and salaries for the employee or employees who get paid the least

**Solution:**
```sql
SELECT TOP (1) WITH TIES employee_id, first_name, last_name, salary
FROM hcm.employees
ORDER BY salary ASC;
```

## WHERE Challenges ##

### Challenge 1 ###
* Select all products which have a price greater than $100:

**Solution:**
```sql
SELECT *
FROM oes.products
WHERE list_price > 100;
```

### Challenge 2 ###
* Select all unshipped orders (i.e. where shipped_date is null):

**Solution:**
```sql
SELECT *
FROM oes.orders
WHERE shipped_date IS NULL;
```

### Challenge 3 ###
* Select all orders placed on the 26th of February 2020: 

**Solution:**
```sql
SELECT *
FROM oes.orders
WHERE order_date = '20200226';
```

### Challenge 4 ###
* Select all orders placed on or after the 1st of January 2020:

**Solution:**
```sql
SELECT *
FROM oes.orders
WHERE order_date >= '20200101';
```

## Pattern Matching Challenges ##

### Challenge 1 ###
* Select all countries which start with the letter 'N':

**Solution:**
```sql
SELECT *
FROM hcm.countries
WHERE country_name LIKE 'N%';
```

### Challenge 2 ###
* Select all customers who have gmail email addresses:

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

### Challenge 3 ###
* Select all product names which contain the word 'mouse':

**Solution:**
```sql
SELECT product_name
FROM oes.products
WHERE product_name LIKE '%mouse%';
```

### Challenge 4 ###
* Select all product names which end in a number:

**Solution:**
```sql
SELECT product_name
FROM oes.products
WHERE product_name LIKE '%[0-9]';
```

## GROUP BY Challenges ##

### Challenge 1 ###
* How many employees are there in each department?

**Solution:**
```sql
SELECT department_id, COUNT(*) AS employee_count
FROM hcm.employees
GROUP BY department_id;
```

### Challenge 2 ###
* What is the average salary in each department?
* Order by average salary from highest to lowest:

**Solution:**
```sql
SELECT department_id, AVG(salary) AS avg_salary
FROM hcm.employees
GROUP BY department_id
ORDER BY avg_salary DESC;
```

### Challenge 3 ###
*  Give the total number of products on hand at each warehouse.
*  Limit the result to only warehouses which have greater than 5000 product items on hand:

**Solution:**
```sql
SELECT warehouse_id, SUM(quantity_on_hand) as total_products_on_hand
FROM oes.inventories
GROUP BY warehouse_id
HAVING SUM(quantity_on_hand) > 5000;
```

### Challenge 4 ###
* What is the date for the most recent population count for each locality in the bird.anarctic_populations table?

**Solution:**
```sql
SELECT 
	locality, 
	MAX(date_of_count) AS date_of_recent_pop_count
FROM bird.antarctic_populations
GROUP BY locality;
```

### Challenge 5 ###
* What is the date of the most recent population count for each species at each locality in the bird.anarctic_populations table?

**Solution:**
```sql
SELECT 
	locality, 
	species_id,
	MAX(date_of_count) AS date_of_recent_pop_count
FROM bird.antarctic_populations
GROUP BY locality, species_id;
```

## Logical Operator Challenges ##

### Challenge 1 ###
* Select employees from Seattle or Sydney:

**Solution:**
```sql
SELECT *
FROM hcm.employees
WHERE city = 'Seattle' OR city = 'Sydney';
```

### Challenge 2 ###
* Select employees who live in any of the following cities, Seattle, Sydney, Ascot, Hillston:

**Solution:**
```sql
SELECT *
FROM hcm.employees
WHERE city IN ('Seattle', 'Sydney', 'Ascot', 'Hillston');
```

### Challenge 3 ###
* Select employees from Sydney who have a salary greater than $200,000:

**Solution:**
```sql
SELECT *
FROM hcm.employees
WHERE city = 'Sydney' AND salary > 200000;
```

### Challenge 4 ###
* Select employees who live in either Seattle or Sydney city and were hired on or after January 1st 2019:

**Solution:**
```sql
SELECT *
FROM hcm.employees
WHERE (city = 'Seattle' OR city = 'Sydney') AND hire_date >= '20190101';
```

### Challenge 5 ###
* Select products that are not categories 1, 2 or 5:

**Solution:**
```sql
SELECT *
FROM oes.products
WHERE category_id NOT IN (1, 2, 5);
```

## Join Challenges ##

### Challenge 1 ###
* Return employee details for employees who belong to a department:

**Solution:**
```sql
SELECT 
	e.employee_id,
	e.first_name,
	e.last_name,
	e.salary,
	d.department_name
FROM hcm.employees e JOIN hcm.departments d 
ON d.department_id = e.department_id;
```

### Challenge 2 ###
* Return employee details for all employees, including employees who do not belong to a department:

**Solution:**
```sql
SELECT 
	e.employee_id,
	e.first_name,
	e.last_name,
	e.salary,
	d.department_name
FROM hcm.employees e LEFT JOIN hcm.departments d 
ON d.department_id = e.department_id;
```

### Challenge 3 ###
* Return the total number of employees in each department.
* Include the department_name in the query result.
* Also, include employees who have not been assigned to a department:

**Solution:**
```sql
SELECT 
	d.department_name,
	COUNT(*) AS employee_count
FROM hcm.employees e LEFT JOIN hcm.departments d 
ON d.department_id = e.department_id
GROUP BY d.department_name;
```

## Advanced Join Challenges ##

### Challenge 1 ###
* Write a query to return employee details for all employees as well
as the first and last name of each employee's manager. \
Include the following columns: \
&ndash; employee_id \
&ndash; first_name \
&ndash; last_name \
&ndash; manager_first_name (alias for first_name) \
&ndash; manager_last_name (alias for last_name)

**Solution:**
```sql
SELECT 
	e.employee_id,
	e.first_name,
	e.last_name,
	e.manager_id,
	m.first_name as manager_first_name,
	m.last_name as manager_last_name
FROM hcm.employees e
LEFT JOIN hcm.employees m
ON e.manager_id = m.employee_id;
```

### Challenge 2 ###
* Write a query to return all the products at each warehouse. \
Include the following attributes: \
&ndash; product_id \
&ndash; product_name \
&ndash; warehouse_id \
&ndash; warehouse_name \
&ndash; quantity_on_hand 

**Solution:**
```sql
SELECT 
	p.product_id,
	p.product_name,
	w.warehouse_id,
	w.warehouse_name,
	i.quantity_on_hand
FROM oes.products p
INNER JOIN oes.inventories i
ON p.product_id = i.product_id
INNER JOIN oes.warehouses w
ON w.warehouse_id = i.warehouse_id;

```
## Function Challenges ##

### Challenge 1 ###
* Concatenate employee first and last names together:

**Solution:**
```sql
SELECT
	employee_id,
	first_name,
	last_name,
	CONCAT(first_name, ' ', last_name)  AS employee_name
FROM hcm.employees;
```

### Challenge 2 ###
* Concatenate employee first, middle, and last names together:

**Solution:**
```sql
SELECT 
	employee_id,
	first_name,
	middle_name,
	last_name,
	CONCAT(first_name, ' ' + middle_name, ' ', last_name) AS employee_name
FROM hcm.employees;
```

### Challenge 5 ###
* Return the age in years for all employees:

**Solution:**
```sql
SELECT
	employee_id,
	first_name,
	last_name,
	birth_date,
	DATEDIFF(year, birth_date, CURRENT_TIMESTAMP) AS employee_age
FROM hcm.employees;
```

### Challenge 6 ###
* Assuming an estimated shipping date of 7 days after the order date.
  Add a column expression called estimated_shipping_date for all unshipped orders

**Solution:**
```sql
SELECT 
	order_id,
	order_date,
	DATEADD(day, 7, order_date) AS estimated_shipping_date
FROM oes.orders
WHERE shipped_date IS NULL;
```

