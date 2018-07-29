## Data step v Proc SQL

Both the Data Step and Proc SQL can slice and dice your data, but which one do you choose?

The short answer is, it depends.

The Data Step works sequentially so will work through each observation one by one to do your merge, whereas PROC SQL doesn't care what order your data is in so in some cases can be more efficient.
If your data set is small it may be worth using the Data Step as all results are returned in order but if you are working with something larger consider PROC SQL.  Either way, SQL is common and a good skill to have.
In this post you'll learn how to subset, sort, group, eliminate duplicates, and combine data using PROC SQL alongside the SAS snippet.

### Creating a subset v Creating a table

```sas
data employeedata2;
set employeedata;
where 20000 <= salary <= 40000;
run;
```

```sql
proc sql;
create table employeedata2 as
select * /* the asterix returns all columns from the table */
from employeedata
where salary BETWEEN 20000 and 40000;
quit; /* use quit instead of run */
```

### Sorting a dataset v Sorting a table

```sas
proc sort data=partnerdata; by clientcapacity; run;
```

```sql
proc sql;
create table partnerdata2 as
select *
from partnerdata
order by clientcapacity; /* the default is ascending
but can be changed to descending using DESC */
quit;
```

### Deduping a dataset v Select Distinct

```sas
proc sort data=customerdata nodupkey out=customerdata2; 
/* optional new table as output */
by customerid;
run;
```

```sql
proc sql;
create table customerdata2 as
select distinct *
from customerdata
order by customerid;
quit;
```

### Merging v INNER JOIN

```sas
proc sort data=students1; BY id; run;
proc sort data=students2; BY id; run;
data students3;
merge students1 ( in= a)
students2 ( in= b );
by id;
if a and b;
run;
```

```sql
proc sql;
create table students3 as
select students1.id, students2.name students2.age
from students1
inner join students2 /* inner join returns results
where the id variable appears in both tables*/
on students1.id = students2.id;
quit;
```

### Merging v LEFT JOIN

```sas
proc sort data=students1; BY id; run;
proc sort data=students2; BY id; run;
data students3;
merge students1 ( in= a)
students2;
by id;
if a ;
run;
```

```sql
proc sql;
create table students3 as
select students1.id, students2.name students2.age
from students1
left join students2 /* left join returns all results
from the 'left' table and leaves a blank where the
variable does NOT appear in both tables*/
on students1.id = students2.id;
quit;
```
