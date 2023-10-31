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

First we'll create the table:

```
CREATE TABLE supermarket_sales
(
 cust_id bigserial,
 cust_name text,
 item text,
 price int
);
```

Left click on tables and refresh to see the new table created.

Now left click on the table and click "import/export data".


