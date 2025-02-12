# HW3: Data Cleaning (Due 2/21/2025)

This assignment will focus broadly on data cleaning, which encompases a set of techniques and tasks to maximize the utility analysts can extract from their data or merge different datasets together.  

In general, data engineers and analysts will be working on datasets gathered from different sources, and each source may have their own way of representing data, their own methodology of collecting data, and their own error tolerances. As such, the different datasets you work with may not be immediately joinable, unionable, or otherwise usable together. 

To handle this issue, there are a range of *data cleaning* techniques that people employ to enable them to work through these differences in datasets. 

In this assignment you will be given three data files (uploaded to Canvas under `Modules > HW3`) which are modified versions of the NYC Taxi dataset. Your goal is to: 
1. merge these files into one single table,
2. impute missing data,
3. write and run SQL queries over this newly merged table.

In order to merge these files into a single table, you will need to resolve formatting differences between the columns in the files. Once these issues are resolved, you should be able to merge these into a single relational table using a `UNION ALL` command. Details and hints about how to find and resolve these formatting differences are in later sections of the assignment.

Next, you will find that a number of values are missing from the `trip_distance` column, preventing those rows from being used in the answers to questions 2 and 3 below. To enable not losing lots of data with NULL values, analysts use [data imputation methods](https://scikit-learn.org/stable/modules/impute.html#multivariate-feature-imputation) which serve to fill in these blank values with data. While you are welcome to utilize more complex methods for data imputation, we will focus on simple methods of data imputation, which replace missing values in a numeric column with the mean, median, or mode of the non-NULL values in the column. 

You can find details on how to handle this step below, including what systems you can use and some suggestions on how to go about it.

Finally, you must answer the three questions written below. We expect that you will have merged your data in step 1, created a new table with the merged data, and then write SQL queries to answer these three questions over that merged table (with NULL values in `trip_distance` replaced). I will not be providing you with the queries: instead you will need to develop the SQL queries and provide both the queries and output as part of your writeup.


# Submission
## Where to Submit
Accept the Github classroom link for HW3 posted on Ed. This will create a Github repo for you. Then, push your writeup and any code you wrote to that repo.

## Writeup Requirements 
Include the following information:
1. What schema/format incompatibilities you found across the 3 files
2. What steps you took to resolve the formatting issues
3. What data imputation strategy you chose for the NULL values in `trip_distance`
4. The SQL queries you authored to answer the questions posed below and their output
5. Any feedback you have on the assignment, relative difficulty, or other information.


# Assignment Description
## Data Files
There are three data files (file1.parquet, file2.parquet, file3.parquet) that you can download from Canvas under `Modules > HW3`. These files have the same set of columns names, though the same columns may have different types across files. Your goal is to be able to UNION these files into a single table. It's your job to investigate these files and schemas to see in what ways the data represented in these files are incompatible with each other and then fix these incompatibilities. You can use *any* SQL engine to clean this data, including BigQuery or Databricks in the cloud, or DuckDB either on cloud infrastructure or on your local computer.

### Hints on how to get started
Look at column types across the three files and see if the same column name has a different type in the different files. Look at how the values are represented. 

Also, one column has also been added, `trip_distance_unit`, which is a string representation of the unit that `trip_distance` is stored in (i.e. `mi` to represent miles.

You will need to use transformation functions like `CAST` ([BigQuery reference](https://cloud.google.com/bigquery/docs/reference/standard-sql/conversion_functions#cast)) to handle format changes, and then will need to update the existing column. One way you can do this is by using [ UPDATE TABLE ADD COLUMN](https://stackoverflow.com/questions/71907295/sql-big-query-add-new-column-to-table-with-query-results) command. These references are to BigQuery, but these commands are also possible in other databases.

## Missing Data Imputation
Once your data has been formatted so that you can create a single merged table, you will need to impute the NULL values in the `trip_distance` column. If you have been using BigQuery so far, or wish to migrate your data to BigQuery for this step, you can use the [ML Imputer Function](https://cloud.google.com/bigquery/docs/reference/standard-sql/bigqueryml-syntax-imputer) which will allow you to select a simple strategy for imputation and specify the column. 

You can then either use the UPDATE TABLE command again, or use this function directly in the SQL query answers to the three questions below.

For other DBs, like Databricks or DuckDB, you can do this step in Pandas, Numpy, or Sci-kit Learn. This then requires you to write that updated data back to a Parquet file or relational table like a DuckDB or Databricks table. 

## Queries
Answer each question below by writing and running a SQL query (one query per question). 

1. Compute the average passenger count on taxi rides that began between 8am and 9am
2. Compute for each VendorID the total trip distance traveled by taxis of that vendor on rides that ended between 10 and 11pm
3. Compute the average amount tipped on taxi rides that travelled more than 1 mile and had exactly 1 passenger

For questions 1 and 2, look at the `EXTRACT` SQL function with hour--so if a column is named `start` with a value `2025-01-01 14:00:00`, and you wanted to get just the hour value, you could run `EXTRACT('hour' from start)` and it would return `14`. All dates/timestamps are stored with 24-hour time notation, so 10pm would be 22. 
