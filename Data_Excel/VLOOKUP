This function saves you time by looking for a piece of information in a large table of data and pulling that into your new table.  

If we have two tables, one with a list of three users names.  The second with a list of 100 names along with their age.  We want to pull the age of the three users from the large table and put it into the small list of users names.

So instead of manually looking through the large table, you can use the vlookup function to do it for you.





## Getting started


1 - Insert a column to the right of the column you are using as the reference.  This is where your formula and results will go.


2 - Type into your formula bar 
<strong>=VLOOKUP(</strong> and complete the formula using the instructions below.

The formula:  

```
=VLOOKUP(
lookup_value - Reference cell.  The field that is in both sheets.
table_array - The range of columns to look in starting with column containing the reference cell.
index_num - The column number where the result is in the range selected.
range_lookup - Used to chose if it should be an exact match or closest match.  0 for exact and 1 for closest match.

```


## What it means

#### lookup_value
You define a value for the formula to look for - for example, the custName in B2.

#### table_array
It looks for a match of the “lookup_value” in the first column of the “table_array”.  This is where you go to the table you want results returned from and highlight the whole column when the reference is and drag over to where the value you want to be returned is.

#### index_num
It will return the value in the column you specify using the “index_num”.  This is where you need to enter the number of columns the result is from the reference.  In the example, we use the number '2' for the second column away from the reference column.

#### range_lookup
The “range_lookup” is a TRUE or FALSE value. If you put 1 it will give you the closest match. If you put 0 it will only give you an exact match.  It's recommended to use an exact match.



All done!  Remember to copy and 'paste values' to ensure you the results remain and not the formula.  If for any reason your lookup table moves or is deleted, so will your results.




## IFERROR

To hide the #N/A error that VLOOKUP throws when it can't find a value, nest the IFERROR function to catch the error and return any value you like. In the case above it will return 'Not found':

```
=IFFERROR(VLOOKUP(B2,Sheet2!B:C,2,0),"Not found")
```
