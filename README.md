# SQL_Introduction


## 1. Initial Setup
- Setup BigQuery Data Environment 

- Download configuration files for PostgreSQL database setup(PDADMIN)

## 2. Data Exploration

-  Select Statements
- Sorting Outputs
- Record Counts
- Distinct Values
- Identify Deduplicate Records
- Column Value Frequency
- Summary Statistics
- Distribution Functions





## 1. Initial Setup

- Setup BigQuery Data Environment

Important: You do not need to setup a billing acount or pay a single cent to use Google’s free BigQuery Sandbox!

But you need a billing account for Google Cloud Storage.

### 1. BigQuery Sandbox

Visit the official Google guide to setup a free BigQuery Sandbox instance – you can use an existing Gmail account or setup a new one just for the Serious SQL course.

```https://cloud.google.com/bigquery/docs/sandbox```


### 2. Navigating The BigQuery Console

Once you are inside the BigQuery console after setting up the BigQuery Sandbox – click on the COMPOSE A NEW QUERY button.

![Screenshot 2023-10-23 at 13 37 15](https://github.com/AdeolaAdesina/SQL_Introduction/assets/29931071/13394599-b9c9-4ed6-b674-644d3a3f6e07)


Below is a super quick visual guide on how to navigate around the BigQuery console!

![Screenshot 2023-10-23 at 13 38 15](https://github.com/AdeolaAdesina/SQL_Introduction/assets/29931071/1fca9d1e-d94b-4dbc-81db-a985d252cb63)



### 3. Loading Data from Google Cloud Storage.

-  the Query a public dataset with the Google Cloud console

```https://cloud.google.com/bigquery/docs/quickstarts/query-public-dataset-console```

- Load data to Google Cloud Storage

In the Google Cloud console, go to the Cloud Storage Buckets page.

Go to Buckets

In the list of buckets, click on the name of the bucket that you want to upload an object to.

In the Objects tab for the bucket, either:

Drag and drop the desired files from your desktop or file manager to the main pane in the Google Cloud console.

Click the Upload Files button, select the files you want to upload in the dialog that appears, and click Open.





### Example Test Query
After all the code has ran successfully – you can open a new BigQuery tab and run a simple query like the one below:

```SELECT * FROM health.users LIMIT 10```


## 1. Initial Setup

### Download configuration files for PostgreSQL database setup(PDADMIN)

Google search - ```postgresql download```

Hit postgresql.org

Download the windows installer

Launch the installer, give it a password and a port number.

Note that this postgresql installation comes with PGADMIN as well.


Now download the data we will upload to PG-ADMIN:

```
Serious SQL datasets: https://storage.googleapis.com/dwd-datasets/serious-sql/serious-sql.zip

```

Now after the installation, hit start and search postgresql documentation, find the PDADMIN icon.

Open PGADMIN and left click on database to create a new database.

Left click on login/group role to create new permissions.

Now left click on the database and click on 'query tool' to query your new database.

Now create a table:

```
create table employee(empID int, namee varchar(25));
```

Now to check our newly created table:

```
select * from employee;
```

Now create binary file. 

Click on file -> preferences -> paths -> binary paths

Now go to the PGADMIN file location you opened previously, left click and click on properties, then click on open file location,

Copy the path and paste in PGADMIN binary path, and save.

Do the same for PostgreSQL advanced server bianry path.

Video explanation: https://www.youtube.com/watch?v=klEB-URLgmk


## Importing data into postgres/PGADMIN Part 1

Let's import a supermarket sales data into postgres/PGADMIN


Now we have 5 tables.

Customer table:

![Screenshot 2023-10-31 at 16 21 27](https://github.com/AdeolaAdesina/SQL_Introduction/assets/29931071/5b9fe18a-252d-48de-815c-b7f67d2b7ccd)

To create table:

```
CREATE TABLE Customer (
    customer_id serial PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(100),
    phone VARCHAR(20)
);
```

To insert data into table:

```
INSERT INTO Customer (first_name, last_name, email, phone)
VALUES
    ('John', 'Smith', 'john.smith@email.com', '123-456-7890'),
    ('Jane', 'Doe', 'jane.doe@email.com', '987-654-3210'),
    ('Alice', 'Johnson', 'alice@email.com', '555-123-4567');
```



Second table  - Product table

![Screenshot 2023-10-31 at 16 21 46](https://github.com/AdeolaAdesina/SQL_Introduction/assets/29931071/df998036-6135-4656-bb20-4e80845c5dc3)


To create table:

```
CREATE TABLE Product (
    product_id serial PRIMARY KEY,
    product_name VARCHAR(100),
    category_id INT,
    price DECIMAL(10, 2),
    description TEXT
);
```

To insert data into Product table:

```
INSERT INTO Product (product_name, category_id, price, description)
VALUES
    ('Apples', 1, 1.99, 'Fresh red apples'),
    ('Bread', 2, 2.49, 'Whole wheat bread'),
    ('Milk', 3, 2.29, '2% reduced-fat milk'),
    ('Cereal', 3, 3.99, 'Honey nut cereal');
```


Third table - Category table

![Screenshot 2023-10-31 at 16 22 03](https://github.com/AdeolaAdesina/SQL_Introduction/assets/29931071/368ea196-db1e-466d-a8e4-cb1b231e261f)


To create table:

```
CREATE TABLE Category (
    category_id serial PRIMARY KEY,
    category_name VARCHAR(50)
);
```

To insert data into table:

```
INSERT INTO Category (category_name)
VALUES
    ('Fruits'),
    ('Bakery'),
    ('Dairy');
```


Fourth table - Sales Table

![Screenshot 2023-10-31 at 16 22 18](https://github.com/AdeolaAdesina/SQL_Introduction/assets/29931071/0df2777c-c880-4ba9-88a7-434e6ab2239e)


To create table:

```
CREATE TABLE Sales (
    sale_id serial PRIMARY KEY,
    customer_id INT,
    sale_date DATE,
    total_amount DECIMAL(10, 2)
);
```

To insert data into table:

```
INSERT INTO Sales (customer_id, sale_date, total_amount)
VALUES
    (1, '2023-10-10', 15.76),
    (2, '2023-10-11', 8.95),
    (3, '2023-10-12', 24.33);
```


Fifth table - SalesItem table:

![Screenshot 2023-10-31 at 16 22 33](https://github.com/AdeolaAdesina/SQL_Introduction/assets/29931071/965d3aa2-7b5e-4b1c-ae5c-3c06ccb193ff)


To create table:

```
CREATE TABLE SalesItem (
    sale_item_id serial PRIMARY KEY,
    sale_id INT,
    product_id INT,
    quantity INT,
    item_price DECIMAL(10, 2)
);
```

To insert data into table:

```
INSERT INTO SalesItem (sale_id, product_id, quantity, item_price)
VALUES
    (1, 101, 3, 5.97),
    (1, 103, 2, 4.58),
    (2, 102, 1, 2.49),
    (3, 104, 4, 15.96);
```



## 1. Select DISTINCT

In PostgreSQL, the SELECT DISTINCT statement is used to retrieve unique values from a specific column or combination of columns in a table. It eliminates duplicate values, so the result set only contains distinct, non-repeating values.

For example, if you have a "Product" table and want to find the distinct product categories, you can use SELECT DISTINCT as follows:

```
SELECT DISTINCT category_id
FROM Product;
```

Example for Gleaning Insights:

Suppose you have a "Sales" table and you want to find unique sale dates. Using SELECT DISTINCT, you can discover when sales occurred without repeating the same date:

```
SELECT DISTINCT sale_date
FROM Sales;
```

## 2. Where statement.

In PostgreSQL, the WHERE clause is used in a SELECT statement to filter rows based on a specified condition.

Example for Gleaning Insights:

Let's say you have a "Sales" table and you want to find insights about sales that occurred on a specific date. You can use the WHERE clause in combination with SELECT DISTINCT to find unique sale dates for a particular customer. For example:

```
SELECT DISTINCT sale_date
FROM Sales
WHERE customer_id = 1;
```


## 3. Order By.

In PostgreSQL, the ORDER BY clause is used in a SELECT statement to sort the result set based on one or more columns in either ascending (default) or descending order. It is a crucial SQL feature for arranging data in a specific order, which can be beneficial for data analysis and reporting.


Example for Gleaning Insights:

Let's say you have a "Sales" table and you want to analyze the sales data by the total amount spent in descending order to identify the most significant sales. You can use the ORDER BY clause like this:

```
SELECT customer_id, total_amount, sale_date
FROM Sales
ORDER BY total_amount DESC;
```



## 4. And / Or.

In PostgreSQL, AND and OR are logical operators used in conjunction with the WHERE clause to combine multiple conditions to filter rows in a SELECT statement. They allow you to create complex filtering criteria by specifying that all or any of the conditions must be met, respectively.


Example for Gleaning Insights:

Suppose you have a "Sales" table and you want to analyze sales that meet specific criteria. You can use AND and OR to filter the data to extract insights.

A. Using AND:

Let's say you want to find sales where the total amount is greater than $20 and the sale date is in October 2023:

```
SELECT customer_id, total_amount, sale_date
FROM Sales
WHERE total_amount > 20 AND EXTRACT(MONTH FROM sale_date) = 10;
```

In this query, both conditions (total amount > 20 and sale date is in October) must be true for a sale to be included in the result set. This can help you glean insights about sales with high values that occurred in a specific month.


B. Using OR:

Let's say you want to find sales where the total amount is greater than $30 or the sale date is in October 2023:


```
SELECT customer_id, total_amount, sale_date
FROM Sales
WHERE total_amount > 30 OR EXTRACT(MONTH FROM sale_date) = 10;
```

In this query, a sale will be included in the result set if either condition (total amount > 30 or sale date is in October) is true.


## 5. Count

In PostgreSQL, the COUNT function is used to count the number of rows in a table or the number of rows that meet a specific condition in a SELECT statement.


Example for Gleaning Insights:

Let's say you have a "Sales" table and you want to obtain insights about the data using the COUNT function:

A. Counting Total Sales:

You can count the total number of sales in the "Sales" table to get an idea of the overall volume of transactions:


```
SELECT COUNT(*) as total_sales
FROM Sales;
```

This query will provide you with the total number of sales made, which can be useful for various analytical purposes.


B. Counting Sales by Date:

To analyze the distribution of sales across different dates, you can count the number of sales on each date:


```
SELECT sale_date, COUNT(*) as sales_count
FROM Sales
GROUP BY sale_date;
```

This query will give you insights into the distribution of sales over time, helping you identify patterns or peak sales dates.


C. Counting Unique Customers:

If you want to know how many unique customers have made purchases, you can use COUNT(DISTINCT customer_id):

```
SELECT COUNT(DISTINCT customer_id) as unique_customers
FROM Sales;
```

This can help you understand the customer base and customer retention.



## 6. Sum

In PostgreSQL, the SUM function is used to calculate the total sum of numeric values in a specific column or expression. It's a valuable tool for obtaining insights related to the summation of data, which can be crucial for various types of data analysis and reporting.


Example for Gleaning Insights:

Let's say you have a "Sales" table and you want to obtain insights about the total amount spent on sales. You can use the SUM function for various scenarios:

A. Total Sales Amount:

To calculate the total amount spent across all sales:

```
SELECT SUM(total_amount) as total_sales_amount
FROM Sales;
```

This query will give you the overall sum of all sales, providing insight into the total revenue generated.


B. Total Sales Amount by Customer:

To determine the total amount spent by each customer, you can use SUM with grouping by customer:

```
SELECT customer_id, SUM(total_amount) as total_customer_spending
FROM Sales
GROUP BY customer_id;
```

This query provides insights into which customers have spent the most, allowing you to identify high-value customers.



C. Total Sales Amount by Month:

To analyze sales on a monthly basis, you can use SUM with date manipulation to group by month:


```
SELECT EXTRACT(MONTH FROM sale_date) as sale_month, SUM(total_amount) as monthly_sales
FROM Sales
GROUP BY sale_month;
```


This query helps you glean insights into monthly sales patterns and can be used for seasonality analysis.



## 7. Aliases

In PostgreSQL, aliases are used to assign temporary names or labels to columns, expressions, or tables in SQL queries. Aliases make the output of a query more readable and can be especially useful when dealing with complex or calculated data. They provide a way to rename columns, tables, or the results of expressions, making your SQL code more human-friendly.


Example for Gleaning Insights:

Let's say you have a "Sales" table and you want to calculate the total amount spent by customers and rename the column for clarity. You can use aliases for this:




```
SELECT customer_id, SUM(total_amount) AS total_spent
FROM Sales
GROUP BY customer_id
ORDER BY total_spent DESC;
```


Without the Alias:


```
SELECT customer_id, SUM(total_amount) 
FROM Sales
GROUP BY customer_id
ORDER BY total_spent DESC;
```



## 8. Join

In PostgreSQL, and SQL in general, "joins" are used to combine rows from two or more tables based on a related column between them. Joins are a fundamental concept in relational databases, and they allow you to create more comprehensive result sets by connecting data from different tables. PostgreSQL supports several types of joins:


![Screenshot 2023-11-07 at 15 53 33](https://github.com/AdeolaAdesina/SQL_Introduction/assets/29931071/084fb6fc-e285-42ec-be7d-b0af3824eea0)



Example Queries:


### Inner Join - Customer and Sales:

```
SELECT
    c.customer_id,
    c.customer_name,
    s.sale_id,
    s.sale_date
FROM
    Customer c
INNER JOIN Sales s ON c.customer_id = s.customer_id;
```

Insight:

This query can provide a list of customers who made purchases along with details of their sales. You can analyze customer-specific sales data.



### Left Join - Product and SalesItem:

```
SELECT
    p.product_id,
    p.product_name,
    si.quantity,
    si.item_price
FROM
    Product p
LEFT JOIN SalesItem si ON p.product_id = si.product_id;
```

Insight:

This query will show all products, including those that haven't been sold. You can identify products that haven't generated sales or analyze sales for each product.


### Right Join - Sales and SalesItem:

```
SELECT
    s.sale_id,
    s.customer_id,
    si.product_id,
    si.quantity
FROM
    Sales s
RIGHT JOIN SalesItem si ON s.sale_id = si.sale_id;
```


Insight:

This query can help identify sales items that may not be associated with a specific sale. You can analyze incomplete sales data or identify potential data inconsistencies.


### Full Join - Customer and Sales:

```
SELECT
    c.customer_id,
    c.customer_name,
    s.sale_id,
    s.total_amount
FROM
    Customer c
FULL JOIN Sales s ON c.customer_id = s.customer_id;
```

Insight:

This query will show all customers and their sales, including customers who haven't made any purchases. Useful for analyzing customer engagement.



## 9. Union

In PostgreSQL, the UNION operator is used to combine the result sets of two or more SELECT statements into a single result set. The result set will contain all distinct rows from the individual queries, eliminating duplicates. UNION is a powerful tool for merging data from different sources or conditions and can be used to glean insights from diverse data sets.


Let's say you have two tables, "Sales2022" and "Sales2023," and you want to combine the data to analyze sales trends over two years.

```
SELECT sale_date, total_amount
FROM Sales2022
UNION
SELECT sale_date, total_amount
FROM Sales2023
ORDER BY sale_date;
```




## 9. Group By

In PostgreSQL, the GROUP BY clause is used to group rows from a table based on the values in one or more columns. It is commonly used in conjunction with aggregate functions (such as SUM, COUNT, AVG, etc.) to perform summary calculations on the grouped data. The GROUP BY clause is a powerful tool for data analysis, allowing you to create summaries and glean insights from your data.



```
SELECT customer_id, COUNT(*) as order_count, SUM(total_amount) as total_spent
FROM Sales
GROUP BY customer_id;
```




# Class Project 


Below are sample datasets for an e-commerce company based in London, containing five tables: Customer, Product, Order, OrderItem, and Category.

Data Schema:

1. 

Customer Table:

customer_id (Primary Key)
customer_name
email
city
country

```
CREATE TABLE Customer (
    customer_id SERIAL PRIMARY KEY,
    customer_name VARCHAR(100),
    email VARCHAR(100),
    city VARCHAR(50),
    country VARCHAR(50)
);
```

To insert into customer table:

```
INSERT INTO Customer (customer_id, customer_name, email, city, country)
VALUES
    (1, 'John Doe', 'john.doe@email.com', 'London', 'United Kingdom'),
    (2, 'Alice Smith', 'alice.smith@email.com', 'London', 'United Kingdom'),
    (3, 'Bob Johnson', 'bob.johnson@email.com', 'Manchester', 'United Kingdom'),
    (4, 'Emma Davis', 'emma.davis@email.com', 'Birmingham', 'United Kingdom'),
    (5, 'Michael Wilson', 'michael.wilson@email.com', 'London', 'United Kingdom'),
    (6, 'Sophie Brown', 'sophie.brown@email.com', 'Edinburgh', 'United Kingdom'),
    (7, 'James White', 'james.white@email.com', 'London', 'United Kingdom'),
    (8, 'Olivia Taylor', 'olivia.taylor@email.com', 'Manchester', 'United Kingdom'),
    (9, 'Daniel Harris', 'daniel.harris@email.com', 'London', 'United Kingdom'),
    (10, 'Emily Hall', 'emily.hall@email.com', 'Birmingham', 'United Kingdom');

```




2.

Product Table:

product_id (Primary Key)
product_name
price
category_id (Foreign Key)

```
CREATE TABLE Product (
    product_id SERIAL PRIMARY KEY,
    product_name VARCHAR(100),
    price DECIMAL(10, 2),
    category_id INT,
    FOREIGN KEY (category_id) REFERENCES Category(category_id)
);
```


To insert data into product table:

```
INSERT INTO Product (product_id, product_name, price, category_id)
VALUES
    (1, 'Laptop', 1200.00, 1),
    (2, 'Smartphone', 800.00, 1),
    (3, 'Headphones', 100.00, 2),
    (4, 'Camera', 600.00, 3),
    (5, 'Printer', 300.00, 3),
    (6, 'Tablet', 500.00, 1),
    (7, 'Mouse', 20.00, 2),
    (8, 'Keyboard', 30.00, 2),
    (9, 'External Hard Drive', 80.00, 3),
    (10, 'Monitor', 250.00, 1);

```




3.

Order Table:

order_id (Primary Key)
customer_id (Foreign Key)
order_date


```
CREATE TABLE Order (
    order_id SERIAL PRIMARY KEY,
    customer_id INT,
    order_date DATE,
    FOREIGN KEY (customer_id) REFERENCES Customer(customer_id)
);
```

To insert data into Order table:



```
INSERT INTO "Order" (order_id, customer_id, order_date)
VALUES
    (1, 1, '2023-11-01'),
    (2, 2, '2023-11-02'),
    (3, 3, '2023-11-02'),
    (4, 1, '2023-11-03'),
    (5, 4, '2023-11-03'),
    (6, 5, '2023-11-04'),
    (7, 2, '2023-11-05'),
    (8, 3, '2023-11-05'),
    (9, 1, '2023-11-06'),
    (10, 4, '2023-11-07');

```

4. 

OrderItem Table:

order_item_id (Primary Key)
order_id (Foreign Key)
product_id (Foreign Key)
quantity
total_price

To create table:

```
CREATE TABLE OrderItem (
    order_item_id SERIAL PRIMARY KEY,
    order_id INT,
    product_id INT,
    quantity INT,
    total_price DECIMAL(10, 2),
    FOREIGN KEY (order_id) REFERENCES Order(order_id),
    FOREIGN KEY (product_id) REFERENCES Product(product_id)
);
```

```
INSERT INTO OrderItem (order_item_id, order_id, product_id, quantity, total_price)
VALUES
    (1, 1, 1, 2, 2400.00),
    (2, 2, 3, 1, 100.00),
    (3, 3, 5, 3, 1800.00),
    (4, 4, 2, 1, 800.00),
    (5, 5, 4, 2, 1200.00),
    (6, 6, 1, 1, 1200.00),
    (7, 7, 8, 1, 30.00),
    (8, 8, 6, 2, 1000.00),
    (9, 9, 9, 1, 80.00),
    (10, 10, 7, 1, 20.00);

```

5.

Category Table:
category_id (Primary Key)
category_name


```
CREATE TABLE Category (
    category_id SERIAL PRIMARY KEY,
    category_name VARCHAR(50)
);
```

To insert data into category table:

```
INSERT INTO Category (category_id, category_name)
VALUES
    (1, 'Electronics'),
    (2, 'Accessories'),
    (3, 'Peripherals');
```

Questions:

Customer Analysis:

- Identify the top 5 customers who have spent the most on orders.
- Provide their names, email addresses, and total amount spent.
  
Product Performance:

- Find the top 3 best-selling products by quantity.
- Include the product names, total quantity sold, and the category of each product.
  
Order Analysis:

- Determine the total revenue generated for each month in the last year.
- Present the results with the month and the corresponding total revenue.






