# HW3: Data Cleaning(Due XX)
This assignment will focus on data cleaning. There are many reasons that data from different sources (or even the same one) may have incompatibilities: different standards for certain types of data (i.e. how to represent null values), error in sensors causing different levels of precision, different processing software using strings vs. dates to represent data. In this assignment, you will be given 3 files originally drawn from the NYC yellow-cab taxi dataset but modified by me. These three files have similar, but not identical, schemas. One column has also been added, `trip_distance_unit` which is a string representation of the unit that `trip_distance` is stored in. You will need to modify these files (using whatever means you like--SQL, pandas, whatever) so that the three files can be merged and queried over together. 

Finally, I have asked three questions below. You will need to write SQL queries over these merged files that answer these questions. I will provide you with the expected output, but not the queries themselves. You will need to provide your SQL queries as part of the writeup. 


# Submission
## Where to Submit
Accept the Github classroom link for HW3 posted on Ed. This will create a Github repo for you. Then, push your writeup and any code you wrote to that repo.

## Writeup Requirements 
Include the following information:
1. What schema/format incompatibilities you found across the 3 files
2. What cleaning steps you took to make the schemas agree
3. The SQL queries you authored to answer the questions posed below (?)
4. Any feedback you have on the assignment, relative difficulty, or other information.


# Assignment Description
## Data Files
There are three data files (file1.parquet, file2.parquet, file3.parquet) that have the same set of columns though columns may have different types. Your goal is to be able to run a single query over all three files (as though we UNION'ed them together). It's your job to investigate these files and schemas to see in what ways the data represented in these files are incompatible with each other and then fix these incompatibilities. You can use *any* way to clean this data, whether it be in a SQL engine like BigQuery, Databricks, or DuckDB or using Python libraries like PyArrow, Pandas, or Spark. 

### Hints on how to get started
Look at column types across the three files and see if the same column has a different type in the different files. Also, take a look at the added `trip_distance_unit` column, which tells you the unit for the `trip_distance` column.  

## Queries
### Query Descriptions
Answer each question below by writing and running a SQL query (one query per question). 

1. Compute the average passenger count on taxi rides that began between 8am and 9am
2. Compute for each VendorID the total trip distance traveled by taxis of that vendor on rides that ended between 10 and 11pm
3. Compute the average amount tipped on taxi rides that travelled more than 1 mile and had exactly 1 passenger

For questions 1 and 2, look at the `EXTRACT` SQL function with hour--so if a column is named `start` with a value `2025-01-01 14:00:00`, and you wanted to get just the hour value, you could run `EXTRACT('hour' from start)` and it would return `14`. All dates/timestamps are stored with 24-hour time notation, so 10pm would be 22. 
### Query Results
This is the expected output. If there's slight differences due to floating point error that's fine.

#### Query 1
| avg |
|-------|
| 1.2869777901295123 |

#### Query 2
|VendorID| total_trip_distance|
|--------|--------------------|
|1| 2817498.4000000088|
|2| 11408353.710000077|
|6| 1565.1299999999997|


#### Query 3
| avg |
|-----|
|4.055592348311921|

