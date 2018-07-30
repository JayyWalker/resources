# Five Tips For Better SQL
Here are five quick tips to improve your query performance and simplify your schemas.

## 1. Keep Column And Table Names Simple
Use one word for a table name instead of two.  If you do need to use multiple words use underscores instead of spaces or full stops.
Having dots in names of objects will cause confusion between schema and database names and using spaces means you need to add quotes in your query to make it run.
Keep column and table names consistently in lowercase so users don’t have to remember which is which if you move to a database which is case sensitive.


## 2. Dealing With Dates In SQL
Convert dates to datetimes to improve performance. It’s harder to work with dates that are stored as strings so make sure these never represent dates.
Don’t split out the year, month, and day in separate columns. This makes queries much harder to write and filter.
Always use UTC for your timezone.  If you have a mix of non-UTC and UTC it makes understanding the data much more difficult.


## 3. Understanding The Order Of Execution
Understanding query order can help you understand how a query runs or worse, why your query won’t run.

- FROM – This includes any JOINs so if you are writing a large query with multiple tables consider using a CTE or subquery to do any filtering first.
- WHERE – To limit the joined dataset.
- GROUP BY – Collapses fields down with aggregate functions (COUNT, MAX, MIN, SUM, AVG) to group the result-set by one or more columns
- HAVING – Performs the same function as the WHERE clause, but with aggregate values in the GROUP BY
- SELECT – Specifies the values and aggregations remaining in the data set after the grouping and pruning have occurred.
- ORDER BY – Returns the table sorted by a column or multiple columns.
- LIMIT – Specifies how many rows you want to be returned and can avoid returning too much data.


## 4. The Limitations Of NULL
NULL means that the value is unknown, not zero and not blank.  This makes it difficult to compare values if you are comparing NULLs with NULLs.
Depending on what you are asking your code to do, influences the strategy you need to take.  Read more about NULLs and how to tackle the problem.


## 5. KNOW HOW TO CREATE A TABLE
When creating a table from a table use SELECT TOP 0 to create the structure of a table before inserting the data into it. It takes two steps instead of one but slashes processing time.
select top 0 * into <table name2>
From <table name1>

```sql
insert into <table name2>
select [ID]
,[CreatedDate]
,[RegionName]
,[SalesPerson]
from <table name1 >
 ```

If updating a table with new data use the TRUNCATE command. It deletes all of the rows from the table without deleting the format and headers

```sql
truncate table <table name1> -- deletes the contents of the table
insert into <table name1>
select [ID]
,[CreatedDate]
,[RegionName]
,[SalesPerson]
from ...
```
