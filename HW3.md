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
### Hints on how to get started
## Queries
### Query Descriptions
Answer each question below by writing and running a SQL query (one query per question). 

1. Avg count of passengers for transactions that occurred between 8 and 9am
2. Total trip distance for each vendor on rides between 10 and 11pm
3. Avg tipped on rides with > 1 mile distance and passenger count == 1

### Query Results

