# SQL_Introduction


## 1. Initial Setup
- Setup BigQuery Data Environment 

- Download configuration files for PostgreSQL database setup(PDADMIN)

## 2. Data Exploration

-  Select Statements
- Sorting Outputs
- Record Counts
- Distinct Values
- Column Value Frequency
- Identify Deduplicate Records
- Summary Statistics
- Distribution Functions

## 3. Marketing Analytics Case Study
3.1. Database Exploration

- Identify key columns of interest and how they are linked to other tables via foreign keys
- Use entity relationship diagrams (ERDs) to analyze the data types for different columns in database tables
- Understand data context for various tables that cause inherent natural relationships between fields

3.2. Table Joins
- Basic joins: INNER JOIN, LEFT JOIN, CROSS JOIN
- Advanced Joins: LEFT SEMI JOIN, ANTI JOIN
- Combination set operations: UNION, UNION ALL, INTERSECT, EXCEPT
- Join multiple tables to combine disparate datasets into a single data structure
- Design a simple framework to identify which type of table join to use for different situations
- Learn a split, group by and merge strategy to combine multi-level calculations for complex data analysis
- Perform table joins that use 2 or more table references in the ON condition
- Using anti joins to exclude records

3.3. Window Functions
- Understand the fundamentals of window functions
- Describe the differences between window functions and group by aggregates
- Identify the different SQL functions which can be used as window functions
- Effectively rank and order records, dealing with equal ties in the process
- Understand the impact of window frame clauses to various window function calculations
- Combine multiple window calculations into a single query for efficient data processing
- Demonstrate how to use window functions for row based calculations such as cumulative sums, rolling metrics
- Calculate weighted moving averages using window functions
- Calculate exponential moving averages using recursive CTEs

3.4. Project Template & SQL Scripting
- Effectively structure and communicate your knowledge and experience through a complete case study write-up
- Learn by example and see the PEAR project structure in action to maximise readibility and impact on readers
- Take your readers on a storytelling journey with mixed technical code and written outputs to demonstrate core SQL skills
- Combine multiple operations and components into a single executable SQL script
- Handle complex logic and maintain code quality to improve readibility, reliability and minimise risk of coding errors



 
3.5. Example Visual Outputs




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


### 4. Initialization Script


Please copy and paste this entire code chunk directly into your BigQuery console and hit the RUN button or CMD / CTRL + ENTER to run all the initialiazation SQL queries!

Be warned, this script is a little lengthy!

```
-- Create all relevant schemas for Serious SQL datasets
CREATE SCHEMA dvd_rentals;
CREATE SCHEMA health;
CREATE SCHEMA employees;
CREATE SCHEMA optimization;
CREATE SCHEMA trading;

-- Create all schemas for 8 Week SQL Challenge datasets
CREATE SCHEMA dannys_diner;
CREATE SCHEMA pizza_runner;
CREATE SCHEMA foodie_fi;
CREATE SCHEMA data_bank;
CREATE SCHEMA data_mart;
CREATE SCHEMA clique_bait;
CREATE SCHEMA balanced_tree;
CREATE SCHEMA fresh_segments;

------------------------
-- Serious SQL Datasets
------------------------

-- Load all required tables for `hedvd_rentals` schema
LOAD DATA OVERWRITE dvd_rentals.customer
FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/dvd_rentals/customer.csv']
);

LOAD DATA OVERWRITE dvd_rentals.actor
FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/dvd_rentals/actor.csv']
);
  
LOAD DATA OVERWRITE dvd_rentals.actor_info
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/dvd_rentals/actor_info.csv']
);

LOAD DATA OVERWRITE dvd_rentals.address
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/dvd_rentals/address.csv']
);

LOAD DATA OVERWRITE dvd_rentals.address
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/dvd_rentals/address.csv']
);

LOAD DATA OVERWRITE dvd_rentals.city
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/dvd_rentals/city.csv']
);

LOAD DATA OVERWRITE dvd_rentals.country
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/dvd_rentals/country.csv']
);

LOAD DATA OVERWRITE dvd_rentals.customer_list
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/dvd_rentals/customer_list.csv']
);

LOAD DATA OVERWRITE dvd_rentals.film
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/dvd_rentals/film.csv']
);

LOAD DATA OVERWRITE dvd_rentals.film_actor
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/dvd_rentals/film_actor.csv']
);

LOAD DATA OVERWRITE dvd_rentals.film_category
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/dvd_rentals/film_category.csv']
);

LOAD DATA OVERWRITE dvd_rentals.film_list
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/dvd_rentals/film_list.csv']
);

LOAD DATA OVERWRITE dvd_rentals.inventory
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/dvd_rentals/inventory.csv']
);

LOAD DATA OVERWRITE dvd_rentals.language
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/dvd_rentals/language.csv']
);

LOAD DATA OVERWRITE dvd_rentals.nicer_but_slower_film_list
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/dvd_rentals/nicer_but_slower_film_list.csv']
);

LOAD DATA OVERWRITE dvd_rentals.payment
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/dvd_rentals/payment.csv']
);

LOAD DATA OVERWRITE dvd_rentals.rental
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/dvd_rentals/rental.csv']
);

LOAD DATA OVERWRITE dvd_rentals.sales_by_film_category
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/dvd_rentals/sales_by_film_category.csv']
);

LOAD DATA OVERWRITE dvd_rentals.sales_by_store
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/dvd_rentals/sales_by_store.csv']
);

LOAD DATA OVERWRITE dvd_rentals.staff
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/dvd_rentals/staff.csv']
);

LOAD DATA OVERWRITE dvd_rentals.staff_list
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/dvd_rentals/staff_list.csv']
);

LOAD DATA OVERWRITE dvd_rentals.store
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/dvd_rentals/store.csv']
);

-- Load all required tables for `health` schema
LOAD DATA OVERWRITE health.user_logs
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/health/user_logs.csv']
);

LOAD DATA OVERWRITE health.users
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/health/users.csv']
);

-- Load all required tables for `employees` schema
LOAD DATA OVERWRITE employees.department
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/employees/department.csv']
);

LOAD DATA OVERWRITE employees.department_employee
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/employees/department_employee.csv']
);

LOAD DATA OVERWRITE employees.department_manager
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/employees/department_manager.csv']
);

LOAD DATA OVERWRITE employees.employee
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/employees/employee.csv']
);

LOAD DATA OVERWRITE employees.salary
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/employees/salary.csv']
);

LOAD DATA OVERWRITE employees.title
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/employees/title.csv']
);

-- Load all tables required for `optimization` schema
LOAD DATA OVERWRITE optimization.addresses
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/optimization/addresses.csv']
);

LOAD DATA OVERWRITE optimization.employees
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/optimization/employees.csv']
);

-- Load all tables required for `trading` schema
LOAD DATA OVERWRITE trading.daily_btc
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/trading/daily_btc.csv']
);

LOAD DATA OVERWRITE trading.daily_eth
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/serious-sql/trading/daily_eth.csv']
);

--------------------------------
-- 8 Week SQL Challenge Datasets
--------------------------------

-- Load all required tables for `dannys_diner` schema
LOAD DATA OVERWRITE dannys_diner.members
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/8-week-sql-challenge/dannys_diner/members.csv']
);

LOAD DATA OVERWRITE dannys_diner.menu
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/8-week-sql-challenge/dannys_diner/menu.csv']
);

LOAD DATA OVERWRITE dannys_diner.sales
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/8-week-sql-challenge/dannys_diner/sales.csv']
);

-- Load all required tables for `pizza_runner` schema
LOAD DATA OVERWRITE pizza_runner.customer_orders
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/8-week-sql-challenge/pizza_runner/customer_orders.csv']
);

LOAD DATA OVERWRITE pizza_runner.pizza_names
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/8-week-sql-challenge/pizza_runner/pizza_names.csv']
);

LOAD DATA OVERWRITE pizza_runner.pizza_recipes
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/8-week-sql-challenge/pizza_runner/pizza_recipes.csv']
);

LOAD DATA OVERWRITE pizza_runner.pizza_toppings
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/8-week-sql-challenge/pizza_runner/pizza_toppings.csv']
);

LOAD DATA OVERWRITE pizza_runner.runner_orders
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/8-week-sql-challenge/pizza_runner/runner_orders.csv']
);

LOAD DATA OVERWRITE pizza_runner.runners
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/8-week-sql-challenge/pizza_runner/runners.csv']
);

-- Load all required tables for `foodie_fi` schema
LOAD DATA OVERWRITE foodie_fi.plans
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/8-week-sql-challenge/foodie_fi/plans.csv']
);

LOAD DATA OVERWRITE foodie_fi.subscriptions
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/8-week-sql-challenge/foodie_fi/subscriptions.csv']
);

-- Load all required tables for `data_bank` schema
LOAD DATA OVERWRITE data_bank.plans
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/8-week-sql-challenge/data_bank/customer_nodes.csv']
);

LOAD DATA OVERWRITE data_bank.customer_transactions
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/8-week-sql-challenge/data_bank/customer_transactions.csv']
);

-- Load all required tables for `data_mart` schema
LOAD DATA OVERWRITE data_mart.weekly_sales
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/8-week-sql-challenge/data_mart/weekly_sales.csv']
);

-- Load all required tables for `clique_bait` schema
LOAD DATA OVERWRITE clique_bait.campaign_identifier
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/8-week-sql-challenge/clique_bait/campaign_identifier.csv']
);

LOAD DATA OVERWRITE clique_bait.event_identifier
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/8-week-sql-challenge/clique_bait/event_identifier.csv']
);

LOAD DATA OVERWRITE clique_bait.events
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/8-week-sql-challenge/clique_bait/events.csv']
);

LOAD DATA OVERWRITE clique_bait.page_hierarchy
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/8-week-sql-challenge/clique_bait/page_hierarchy.csv']
);

LOAD DATA OVERWRITE clique_bait.users
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/8-week-sql-challenge/clique_bait/users.csv']
);

-- Load all required tables for `fresh_segments` schema
LOAD DATA OVERWRITE fresh_segments.interest_map
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/8-week-sql-challenge/fresh_segments/interest_map.csv']
);

LOAD DATA OVERWRITE fresh_segments.interest_metrics
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/8-week-sql-challenge/fresh_segments/interest_metrics.csv']
);

LOAD DATA OVERWRITE fresh_segments.json_data
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/8-week-sql-challenge/fresh_segments/json_data.csv']
);

-- Load all required tables for `balanced_tree` schema
LOAD DATA OVERWRITE balanced_tree.product_details
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/8-week-sql-challenge/balanced_tree/product_details.csv']
);

LOAD DATA OVERWRITE balanced_tree.product_hierarchy
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/8-week-sql-challenge/balanced_tree/product_hierarchy.csv']
);

LOAD DATA OVERWRITE balanced_tree.product_prices
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/8-week-sql-challenge/balanced_tree/product_prices.csv']
);

LOAD DATA OVERWRITE balanced_tree.sales
  FROM FILES (
  format = 'CSV',
  uris = ['gs://dwd-datasets/8-week-sql-challenge/balanced_tree/sales.csv']
);
```


### Example Test Query
After all the code has ran successfully – you can open a new BigQuery tab and run a simple query like the one below:

```SELECT * FROM health.users LIMIT 10```


1. Initial Setup

- Download configuration files for PostgreSQL database setup(PDADMIN)

