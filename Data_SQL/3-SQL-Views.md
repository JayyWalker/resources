# SQL Views
Database views are searchable objects in a relational database defined by a query. The view doesn't store data but you can query a view like you can a table.

## Advantages of database view
- Through a database view, you only have to use simple SQL statements instead of complex ones with many joins.
- A view helps limit data access to specific users. You may not want a subset of sensitive data that can be queried by all users.
- Views take very little space to store as they do not store actual data.

## Disadvantages of database view
Querying data from a database view can be slow especially if the view is created based on other views.
You create a view based on underlying tables of the database. Whenever you change the structure of these tables that view associated with, you have to change the view as well.

## Creating a view
```sql
create view
view_name as
select
column1, column2, ...
from
table_name
where condition;
```

## Replacing a view
```sql
create or replace view
view_name as
select
column1, column2, ...
from
table_name
where condition;
```

## Dropping a view
```sql
drop view
view_name;
```
