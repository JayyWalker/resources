SAS gives you the ability to transform your data and perform statistical analysis.  This starter kit shows you how to produce descriptive statistics for your projects

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
