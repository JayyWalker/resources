# Excel


## Text Functions
Excel functions make your life easier to calculate, analyse and clean up data. These five functions convert text so it's consistent.


### PROPER, LOWER, UPPER
To change the case of a cell using one functions insert a new column to the right of your data and use the functions below.  Don't forget to copy and 'Paste Values' to make the values remain.

```
=PROPER(A1)
=LOWER(A1)
=UPPER(A1)
```

### Trim
Sometimes when importing data extra spaces can be added in the process.  To remove these, we use the TRIM function:

```
=TRIM(A1)
``` 

### Concatenate
This function is useful for putting a First Name and Last Name field back together with one step.  Eg Pastes B2 and A2 together in one cell with one space in between.

```
=CONCATENATE(B2," ",A2)
```
