# SAS

[Getting Started](#getting-started)

[Stats with SAS](#stats-with-sas)

[Data step v Proc SQL](#Data-step-v-Proc-SQL)

## Getting Started

### Clear Work Directory
SAS uses a working directory, similar to temp tables in SQL server.  Your tables will live here until you clear them out or when you shut down your SAS window.  Use the code below to start from scratch and clear your work directory before running, or rerunning, your code.  Doing this makes sure you're not using old data or using extra memory to hold unused tables.

```sas
proc datasets library = work kill; run; quit;
```

### Import
This code snippet will import a csv file from the E drive and name it 'datafile'.  'Guessing rows' tells SAS how long the file is to determine the appropriate data type and length of the file.

```sas
proc import out = datafile
datafile = "E:\filepath.csv"
dbms = csv replace;
getnames = YES;
guessingrows = 1000;
run;
```

### Create Dataset
To segment a table further, you use the data step.  This takes the old table and creates a new one in your working directory based on the criteria in the 'if' step.  Like SQL or Excel, you can use SAS functions to change the case of the data.

```sas
data newtable;
set datafile;
firstname = propcase (firstname); 
email = lowcase (email);
if country = 'UK'
run;
```

### Sort and Merge
This is the equivalent of a SQL join.  The first step is for both datasets to be sorted, in this case with the 'nodupkey' which is the SAS way of doing a SELECT DISTINCT.  The second step is to merge the two tables.  In this case, it will be an INNER JOIN, as both the code says the name must be in 'a and b'. The result is created in a new table.

```sas
proc sort data = newtable nodupkey; by firstname; run; 
proc sort data = newtable2 nodupkey; by firstname; run;
data newtable3; 
merge
newtable (in=a)
newtable2 (in=b);
by firstname;
if a and b; /* Set the condition here eg. a and b, a and not b */
run;
```

### Profile and Check
This snippet counts the number of variables the same way we use COUNT DISTINCT in SQL.  It's handy to use this to check how many variables you have as you work through your script.  The now, nocol, nocum and nopercent supress row percentages, column percentages, cumulative frequencies and percentages.

```sas
proc freq data = newtable3;
table firstname / missing norow nocol nocum nopercent;
run; 
```

### Drop fields

```sas
data newtable4;
set newtable3 (keep = email);
run;
```

### Rename fields

```sas
data newtable5;
set newtable4;
rename emailaddress = email;
run;
```

### Export

This snippet produces a csv file and lands it to your chosen file path.

```sas
proc export data = newtable5
outfile = "E:\filepath.csv";
run;
```

## Stats with SAS

### Frequency tables with Proc freq
Creates a frequency tables for all variables

```sas
proc freq data = <tablename>;
table <variable> / <options>;
run;
```
Options :
norow nocol nocum nopercent - suppresses printing of column, row and cell percentages
missing- interprets missing values as non-missing and includes them in % and calculations

```sas
proc freq data=customertable;
table payingflag / missing norow nocol nocum;
run;
```

### Descriptive statistics with Proc means
Provides the number of observations, mean, std, min, and max

```sas
proc means data=<tablename>;
var <variable>;
title <titlename>;
run;
```
Options :
If variable list is not mentioned it gives results across all numeric variables

```sas
proc means data=<tablename>;
var <variable>;
title 'Feb';
run;
```

### Plots with Proc univariate
```sas
proc univariate data=<tablename>;
var <variable>
histogram;
run;
```
Options :
Normal option produces the tests of normality
Plot option produces stem and leaf plot, box plot, normal probability plot
Histogram option gives the distribution of variable in a histogram

```sas
proc univariate data=invoices;
var createddate;
histogram;
header='Invoices';
label='Created Date';
title='Invoices for current month';
run;
```

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
