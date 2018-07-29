Here are four more useful functions to use in Excel.  This time, logical functions that return a result based on the conditions



AND
Returns TRUE if ALL of the arguments evaluate to TRUE

=AND(E2>10, F2<200)


Eg. Returns TRUE if a value in cell E2 is greater than 10, AND a value in F2 is greater than 200







OR
Returns TRUE if ANY of the arguments evaluate to TRUE

=OR(E2>10, F2<200)


Eg. Returns TRUE if a value in cell E2 is greater than 10, OR a value in F2 is greater than 200







NOT
Returns the reversed logical value of its argument. ie. If the argument is FALSE, then TRUE is returned and vice versa

=NOT(E2>50)


Eg. Returns TRUE if a value in E2 is NOT greater than 500







IF
If you want to return a value based on whether a condition has been satisfied, but you don’t want to be limited to just TRUE or FALSE, then you can use the IF function.

The IF function needs 3 parameters:

The test
The result if the test is TRUE
The result if the test is FALSE


=IF(test,"true","false") <- text needs to be in double quotes
=IF(B2>C2;"Win"Lose")
