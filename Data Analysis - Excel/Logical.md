# Excel


## Logical Functions

### AND
Returns TRUE if ALL of the arguments evaluate to TRUE. Eg. Returns TRUE if a value in cell E2 is greater than 10, AND a value in F2 is greater than 200

```
=AND(E2>10, F2<200)
```

### OR
Returns TRUE if ANY of the arguments evaluate to TRUE. Eg. Returns TRUE if a value in cell E2 is greater than 10, OR a value in F2 is greater than 200

```
=OR(E2>10, F2<200)
```

### NOT
Returns the reversed logical value of its argument. ie. If the argument is FALSE, then TRUE is returned and vice versa. Eg. Returns TRUE if a value in E2 is NOT greater than 500

```
=NOT(E2>50)
```

### IF
If you want to return a value based on whether a condition has been satisfied, but you don’t want to be limited to just TRUE or FALSE, then you can use the IF function.

The IF function needs 3 parameters:

- The test
- The result if the test is TRUE
- The result if the test is FALSE

```
=IF(test,"true","false") <- text needs to be in double quotes
=IF(B2>C2;"Win"Lose")
```

Nesting simply means to combine formulas, one inside the other, so that one formula handles the result of another.

```
=IF(B5>1000,"Platinum",
IF(B5>300,"Gold",
IF(B5>75,"Silver",
IF(B5>25,"Bronze",
"Starter"))))
```

### SUMIF
```
=SUMIF(range,"criteria")
=SUMIF(B1:B4,">=40") - to add up only those values in a range
```

### COUNTIF
```
=COUNTIF(range,"criteria")
=COUNTIF(B1:B4,"South Africa") - to count up only those values in a range
```
