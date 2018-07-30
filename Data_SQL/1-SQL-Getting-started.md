# The Relational Model
When working with data in relational databases there are some key concepts to understand.  Data is organised and stored in the form of tables. A database is a collection of data placed in tables.

## Relationship Categories in Databases
- one-to-one: Relationship between one husband and one wife
- many-to-one: Relationship between many students and one school
- one-to-many: Relationship between one customer and many bank accounts
- many-to-many: Relationship between many students and many teachers

## Primary Key v Foreign Key
A primary key is a column that best identifies one unique row, and identifies each record as unique, like an ID

- It ensures that there are no duplicates
- It cannot be empty (NULL)
- There can only be one primary key per table
- A foreign key is a column that matches a primary key in another table so we can join the data in each together.

# Statements
SQL statements are used to transform the data into more segmented tables.  The basics fall into four main groups:

## Retrieve data
```sql
select 
name, address, city, country
/* the columns to return */
from 
customers.address
/* the schema and table to retrieve data from */
where
age = 21
and name = bob
/* filters for specific rows */
```

## Add new data
```sql
insert into 
customers.address (name, address, city, country)
/* where the data is to go */
values
('Bob Jones', '123 Main St', 'Auckland', 'New Zealand');
/* the data that is to go into the columns above */
```

## Remove data
```sql
delete from
customers.address 
/* where the data is to be deleted from */
where
name = 'Bob Jones' 
/* the condition that needs to be met */
```

## Modify data
```sql
update
customers.address 
/* where the data is to be updated */
set
country = 'New Zealand' 
/* the new value or update */
where
city = 'Auckland'; 
/* the condition that needs to be met */
```
