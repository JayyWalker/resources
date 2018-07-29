Here are the basic Javascript data types.  The five primitive data types, strings, variables and operators



The five primitive data types
Number - for doing maths
Boolean - TRUE/FALSE
Undefined - describes something we don't know yet
Null - a placeholder
String - for storing text between a set of double quotes


Anything that doesn’t belong to any of these five primitive types is considered an object and contains more complex data.

Javascript is 'loosely typed' so if you write a number it assumes it is a number, but if you then use it in a string of text it changes it to fit what you are doing.  You don't have to change it manually to fit the task.



Strings
Methods we can perform:

toUpperCase()
toLowerCase()
slice() /* create a new string from a portion of this one */
concat()
replace(a, b)  /* allows you to replace a with b throughout the string */

Variables
Variables store data, like saving a file, so we can use it later.  If we don't, it is considered a 'literal' and can't be used later.  This is called 'Garbage Collection'

var address = "1 Main Street"; /* string variable */
var age = 30; /* number variable */
var married = TRUE; /* boolean variable */

Operators
x == 5  /* tests for the same value */
x === 5  /* tests for the same value and is the same type */
x != 5  /* tests for not the same value */
x !== 5   /* tests for not the same value and same type */

Logical Operators
AND (&&)
expr1 && expr2
Returns expr1 if it can be converted to false; otherwise, returns expr2.  When used with Boolean values, && returns true if both operands are true; otherwise, returns false.



Logical OR (||)
expr1 || expr2
Returns expr1 if it can be converted to true; otherwise, returns expr2.  When used with Boolean values, || returns true if either operand is true; if both are false, returns false.



Logical NOT (!)
!expr
Returns false if its single operand can be converted to true; otherwise, returns true.
