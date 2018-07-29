## SAS

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
