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

![image](https://github.com/AdeolaAdesina/SQL_Introduction/assets/29931071/ac67ffe1-48dd-4779-9cb1-513abe471c3b)


